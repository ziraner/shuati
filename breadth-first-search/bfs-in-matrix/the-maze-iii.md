the Maze III 解题报告

**Description**

There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up (u), down (d), left (l) or right (r), but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction. There is also a hole in this maze. The ball will drop into the hole if it rolls on to the hole.

Given the ball position, the hole position and the maze, find out how the ball could drop into the hole by moving the shortest distance. The distance is defined by the number of empty spaces traveled by the ball from the start position (excluded) to the hole (included). Output the moving directions by using 'u', 'd', 'l' and 'r'. Since there could be several different shortest ways, you should output the lexicographically smallest way. If the ball cannot reach the hole, output "impossible".

The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The ball and the hole coordinates are represented by row and column indexes.

**Note**
1. There is only one ball and one hole in the maze.
2. Both the ball and hole exist on an empty space, and they will not be at the same position initially.
3. The given maze does not contain border (like the red rectangle in the example pictures), but you could assume the border of the maze are all walls.
4. The maze contains at least 2 empty spaces, and the width and the height of the maze won't exceed 30.


**Example**

Example 1:
```
Input:
[[0,0,0,0,0],[1,1,0,0,1],[0,0,0,0,0],[0,1,0,0,1],[0,1,0,0,0]]
[4,3]
[0,1]

Output:
"lul"
```
Example 2:
```
Input:
[[0,0,0,0,0],[1,1,0,0,1],[0,0,0,0,0],[0,1,0,0,1],[0,1,0,0,0]]
[0,0]
[1,1]
[2,2]
[3,3]
Output:
"impossible"
```

**Idea**

 这个题是`the maze II`的又一次变形。主要有两点需要额外考虑的点：1. 加入了hole。判断进了墙之后需要向后退，而判断掉进了hole不需要向后退因为出不来。2. 除了比较distance又加了比较paths的lexicographical order。需要先判断distance，如果distance小于当前则更新；如果distance相同比较paths，如果新的paths小于当前更新入队。

 queue中依旧保存的是integer不需要单独开一个Point的class。

 需要两个二维矩阵一个用来保存distances一个用来保存paths

**Solution**
```java
public class Solution {
    /**
     * @param maze: the maze
     * @param ball: the ball position
     * @param hole: the hole position
     * @return: the lexicographically smallest way
     */
    public String findShortestWay(int[][] maze, int[] ball, int[] hole) {
        // write your code here
        int n = maze.length;
        int m = maze[0].length;
        int[][] distances = new int[n][m];
        String[][] paths = new String[n][m];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                distances[i][j] = Integer.MAX_VALUE;
                paths[i][j] = "";
            }
        }

        Queue<Integer> queue = new LinkedList<>();
        distances[ball[0]][ball[1]] = 0;
        queue.offer(ball[0] * m + ball[1]);

        int[] dx = {-1, 1, 0, 0};
        int[] dy = {0, 0, -1, 1};
        String[] dir = {"u", "d", "l", "r"};

        while(!queue.isEmpty()) {
            int cur = queue.poll();
            int x = cur / m;
            int y = cur % m;
            for (int i = 0; i < dx.length; i++) {
                int newx = x;
                int newy = y;
                while (newx >= 0 && newx < n && newy >= 0 && newy < m && maze[newx][newy] != 1 && (hole[0] != newx || hole[1] != newy)) {
                    newx += dx[i];
                    newy += dy[i];
                }

                // if hit hole, can't go back; if hit wall, go back
                if (newx != hole[0] || newy != hole[1]) {
                    newx -= dx[i];
                    newy -= dy[i];
                }

                int newDist = Math.abs(newx - x) + Math.abs(newy - y) + distances[x][y];
                // distance comparison
                if (distances[newx][newy] < newDist) {
                    continue;
                }
                // path comparison if distances are same
                String newPath = paths[x][y] + dir[i];
                if (distances[newx][newy] == newDist && paths[newx][newy].compareTo(newPath) <= 0) {
                    continue;
                }
                queue.offer(newx * m + newy);
                distances[newx][newy] = newDist;
                paths[newx][newy] = newPath;
            }
        }
        return distances[hole[0]][hole[1]] == Integer.MAX_VALUE ? "impossible" : paths[hole[0]][hole[1]];
    }
}
```
