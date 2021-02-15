Shortest path to the destination 解题报告

**Description**

Given a 2D array representing the coordinates on the map, there are only values 0, 1, 2 on the map. value 0 means that it can pass, value 1 means not passable, value 2 means target place. Starting from the coordinates [0,0],You can only go up, down, left and right. Find the shortest path that can reach the destination, and return the length of the path.

**Note**

The map must exist and is not empty, there is only one target

Example 1
```
Input:
[
 [0, 0, 0],
 [0, 0, 1],
 [0, 0, 2]
]
Output: 4
Explanation: [0,0] -> [1,0] -> [2,0] -> [2,1] -> [2,2]
```

Example 2
```
Input:
[
    [0,1],
    [0,1],
    [0,0],
    [0,2]
]
Output: 4
Explanation: [0,0] -> [1,0] -> [2,0] -> [3,0] -> [3,1]
```

Idea:

最基础的bfs in matrix；需要注意的点有对于二维矩阵而言，可以通过算m*x + y的方式将二维转化为一维压入queue，而不需重新构造Coordinate class

Solution

```java
public class Solution {
    /**
     * @param targetMap:
     * @return: nothing
     */
    public int shortestPath(int[][] targetMap) {
        // Write your code here
        int n = targetMap.length;
        int m = targetMap[0].length;
        int[][] distances = new int[n][m];

        int targetX = 0;
        int targetY = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (targetMap[i][j] == 2) {
                    targetX = i;
                    targetY = j;
                }
                distances[i][j] = -1;
            }
        }

        return bfs(targetX, targetY, targetMap, distances);
    }

    private int bfs(int targetX, int targetY, int[][] targetMap, int[][] distances) {
        int n = targetMap.length;
        int m = targetMap[0].length;

        int startX = 0;
        int startY = 0;

        int[] dx = {-1, 1, 0, 0};
        int[] dy = {0, 0, -1, 1};

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(startX * m + startY);
        distances[0][0] = 0;

        while (queue.size() > 0) {
            int offset = queue.poll();
            int x = offset / m;
            int y = offset % m;
            if (x == targetX && y == targetY) {
                return distances[x][y];
            }

            for (int j = 0; j < dx.length; j++) {
                int newx = x + dx[j];
                int newy = y + dy[j];
                if(newx < 0 || newx >= n || newy < 0 || newy >= m) {
                    continue;
                }
                if(distances[newx][newy] != -1 || targetMap[newx][newy] == 1) {
                    continue;
                }
                distances[newx][newy] = distances[x][y] + 1;
                queue.offer(newx * m + newy);
            }
        }
        return -1;
    }
}
```
