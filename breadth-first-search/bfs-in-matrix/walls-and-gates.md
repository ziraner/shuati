Walls and Gates 解题报告 Lintcode: Nearest Exit

You are given am x n2D grid initialized with these three possible values.

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

```
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



  




