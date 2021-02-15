the Maze I 解题报告

**Description**

There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but **it won't stop rolling until hitting a wall**. When the ball stops, it could choose the next direction.

Given the ball's start position, the destination and the maze, determine whether the ball could stop at the destination.

The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The start and destination coordinates are represented by row and column indexes.

**Note**
1. There is only one ball and one destination in the maze.
2. Both the ball and the destination exist on an empty space, and they will not be at the same position initially.
3. The given maze does not contain border (like the red rectangle in the example pictures), but you could assume the border of the maze are all walls.
4. The maze contains at least 2 empty spaces, and both the width and height of the maze won't exceed 100.

**Example**

Example 1:
```
Input:
map =
[
 [0,0,1,0,0],
 [0,0,0,0,0],
 [0,0,0,1,0],
 [1,1,0,1,1],
 [0,0,0,0,0]
]
start = [0,4]
end = [3,2]
Output:
false
```
Example 2:
```
Input:
map =
[[0,0,1,0,0],
 [0,0,0,0,0],
 [0,0,0,1,0],
 [1,1,0,1,1],
 [0,0,0,0,0]
]
start = [0,4]
end = [4,4]
Output:
true
```

**Idea**

这个题目是`Shortest path of the destination`的变形。注意题目中黑色加粗的部分，小球向一个方向滚的时候只有在遇到阻隔才会停止，而不是一次只移动一格。

对应在分析上就是在取next的时候，要保持小球沿着该方向一直移动直到撞墙，撞墙之后要返回一步，且返回的这一步一定是valid的因为最差情况是返回起点，起点一定是valid所以不需要做valid判断。

其他部分与shortest path类似。

**Solution**
```java
public class Solution {
    /**
     * @param maze: the maze
     * @param start: the start
     * @param destination: the destination
     * @return: whether the ball could stop at the destination
     */
    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        // write your code here
        int n = maze.length;
        int m = maze[0].length;

        boolean[][] visited = new boolean[n][m];

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(start[0] * m + start[1]);
        visited[start[0]][start[1]] = true;

        int[] dx = {-1, 1, 0, 0};
        int[] dy = {0, 0, -1, 1};

        while (queue.size() > 0) {
            int cur = queue.poll();
            if (cur / m == destination[0] && cur % m == destination[1]) {
                return true;
            }

            for (int i = 0; i < dx.length; i++) {
                int next = getNext(cur, maze, dx[i], dy[i]);
                if (visited[next / m][next % m]) {
                    continue;
                }
                queue.offer(next);
                visited[next / m][next % m] = true;
            }
        }
        return false;
    }

    private int getNext(int cur, int[][] maze, int stepX, int stepY) {
        int n = maze.length;
        int m = maze[0].length;
        int x = cur / m;
        int y = cur % m;
        while (x >= 0 && x < n && y >= 0 && y < m && maze[x][y] != 1) {
            x += stepX;
            y += stepY;
        }
        x -= stepX;
        y -= stepY;
        return x * m + y;
    }
}
```
