Walls and Gates 解题报告

You are given a m x n 2D grid initialized with these three possible values.

1. `-1`- A wall or an obstacle.
2. `0` - A gate.
3. `INF`- Infinity means an empty room. We use the value `2^31- 1 = 2147483647 `to represent`INF`as you may assume that the distance to a gate is less than`2147483647`.

Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with`INF`.

For example, given the 2D grid:

```
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
```

After running your function, the 2D grid should be:

```
  3  -1   0   1
  2   2   1  -1
  1  -1   2  -1
  0  -1   3   4
```

思路：矩阵里面的BFS，以每一个gate为起点做BFS，如果当前的distance比原来的小则更新否则不更新

此题不需要额外矩阵，原room矩阵可以直接用来更新

**Solution:**
1. python
```python
class Solution(object):
    def wallsAndGates(self, rooms):
        """
        :type rooms: List[List[int]]
        :rtype: void Do not return anything, modify rooms in-place instead.
        """
        for i in xrange(len(rooms)):
            for j in xrange(len(rooms[0])):
                if rooms[i][j] == 0:
                    self.bfs(rooms, i, j)

    def bfs(self, rooms, i, j):
        delta = [[0, 1], [0, -1], [-1, 0], [1, 0]]
        q = [(i, j)]
        while q:
            x, y = q.pop(0)
            for deltax, deltay in delta:
                xx, yy = x + deltax, y + deltay
                if xx >= 0 and xx < len(rooms) and yy >= 0 and yy < len(rooms[0]) \
                        and rooms[xx][yy] > rooms[x][y] + 1:
                    rooms[xx][yy] = rooms[x][y] + 1
                    q.append((xx, yy))
```
2. java
```java
public class Solution {
    /**
     * @param rooms: m x n 2D grid
     * @return: nothing
     */
    public void wallsAndGates(int[][] rooms) {
        // write your code here
        for (int i = 0; i < rooms.length; i++) {
            for (int j = 0; j < rooms[0].length; j++) {
                if (rooms[i][j] == 0) {
                    bfs(i, j, rooms);
                }
            }
        }
    }

    private void bfs(int startX, int startY, int[][] rooms) {
        int n = rooms.length;
        int m = rooms[0].length;

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(m * startX + startY);

        int[] dx = {-1, 1, 0, 0};
        int[] dy = {0, 0, -1, 1};

        while(!queue.isEmpty()) {
            int cur = queue.poll();
            int x = cur / m;
            int y = cur % m;
            for (int i = 0; i < dx.length; i++) {
                int newx = x + dx[i];
                int newy = y + dy[i];
                if (newx < 0 || newx >= n || newy < 0 || newy >= m) {
                    continue;
                }

                int newDist = rooms[x][y] + 1;
                if (newDist >= rooms[newx][newy]) {
                    continue;
                }

                rooms[newx][newy] = newDist;
                queue.offer(newx * m + newy);
            }
        }
    }
}
```
