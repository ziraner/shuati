the Maze II 解题报告

**Description**

There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the ball's start position, the destination and the maze, find the shortest distance for the ball to stop at the destination. The distance is defined by the number of empty spaces traveled by the ball from the start position (excluded) to the destination (included). If the ball cannot stop at the destination, return -1.

The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The start and destination coordinates are represented by row and column indexes.


**Note**
1. There is only one ball and one destination in the maze.
2. Both the ball and the destination exist on an empty space, and they will not be at the same position initially.
3. The given maze does not contain border (like the red rectangle in the example pictures), but you could assume the border of the maze are all walls.
4. The maze contains at least 2 empty spaces, and both the width and height of the maze won't exceed 100.

**Example**
```
Example 1:
	Input:  
	(rowStart, colStart) = (0,4)
	(rowDest, colDest)= (4,4)
	0 0 1 0 0
	0 0 0 0 0
	0 0 0 1 0
	1 1 0 1 1
	0 0 0 0 0

	Output:  12

	Explanation:
	(0,4)->(0,3)->(1,3)->(1,2)->(1,1)->(1,0)->(2,0)->(2,1)->(2,2)->(3,2)->(4,2)->(4,3)->(4,4)

Example 2:
	Input:
	(rowStart, colStart) = (0,4)
	(rowDest, colDest)= (0,0)
	0 0 1 0 0
	0 0 0 0 0
	0 0 0 1 0
	1 1 0 1 1
	0 0 0 0 0

	Output:  6

	Explanation:
	(0,4)->(0,3)->(1,3)->(1,2)->(1,1)->(1,0)->(0,0)
```

**Idea**

这个题目与`the maze I`的不一样之处在于需要求shortest distances

基本思路是按照I来的，需要注意的是将boolean[][]改成int[][]，且初始化为MAX_VALUE。这样可以将访问过与否与更新当前distance与否通过一次比较来实现。

queue中保存的依旧可以是offset过的integer值。

**Solution**
```java
public class Solution {
    /**
     * @param maze: the maze
     * @param start: the start
     * @param destination: the destination
     * @return: the shortest distance for the ball to stop at the destination
     */
    public int shortestDistance(int[][] maze, int[] start, int[] destination) {
        // write your code here
        int n = maze.length;
        int m = maze[0].length;

        int[][] distances = new int[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                distances[i][j] = Integer.MAX_VALUE;
            }
        }

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(start[0] * m + start[1]);
        distances[start[0]][start[1]] = 0;

        int[] dx = {-1, 1, 0, 0};
        int[] dy = {0, 0, -1, 1};

        while (!queue.isEmpty()) {
            int cur = queue.poll();
            int x = cur / m;
            int y = cur % m;
            for (int i = 0; i < dx.length; i++) {
                int newx = x;
                int newy = y;
                while (newx >= 0 && newx < n && newy >= 0 && newy < m && maze[newx][newy] != 1) {
                    newx += dx[i];
                    newy += dy[i];
                }
                newx -= dx[i];
                newy -= dy[i];

                int newDist = Math.abs(newx - x) + Math.abs(newy -y) + distances[x][y];
                if (newDist < distances[newx][newy]) {
                    distances[newx][newy] = newDist;
                    queue.offer(newx * m + newy);
                }
            }
        }

        return distances[destination[0]][destination[1]] == Integer.MAX_VALUE ? -1 : distances[destination[0]][destination[1]];
    }
}
```
