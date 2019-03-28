Number of Islands 解题报告

Given a 2d grid map of`'1'`s \(land\) and`'0'`s \(water\), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
11110


11010


11000


00000
```

Answer: 1

**Example 2:**

```
11000


11000


00100


00011
```

Answer: 3

Idea:

BFS: O\(m \* n\)时间复杂度somehow leetcode过不了

```
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid or not grid[0]:
            return 0
        cnt = 0
        for i in xrange(len(grid)):
            for j in xrange(len(grid[0])):
                if grid[i][j] == '1':
                    cnt += 1
                    self.bfs(grid, i, j)
        return cnt
    def bfs(self, grid, i, j):
        delta = [[1, 0], [-1, 0], [0, -1], [0, 1]]
        q = [(i, j)]
        while q:
            x, y = q.pop(0)
            grid[x][y] = '0'
            for deltax, deltay in delta:
                newx, newy = x + deltax, y + deltay
                if newx < 0 or newx >= len(grid) or newy < 0 or newy >= len(grid[0]):
                    continue
                if grid[newx][newy] == '0':
                    continue
                q.append((newx, newy))
```

UnionFind: O\(m \* n\)时间复杂度

在unionfind中定义一个count跟connecting graph III类似数一下当前时候孤岛的数量

整体岛屿的数量 = 1的个数 - （初始m\*n个孤岛 - 当前孤岛的数量）

```
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid or not grid[0]:
            return 0
        m, n = len(grid), len(grid[0])
        uf = UnionFind(m * n)
        cnt = 0
        for i in xrange(m):
            for j in xrange(n):
                if grid[i][j] == '1':
                    cnt += 1
        delta = [[0, 1], [0, -1], [1, 0], [-1, 0]]
        for i in xrange(m):
            for j in xrange(n):
                if grid[i][j] == '1':
                    for deltax, deltay in delta:
                        ii, jj = i + deltax, j + deltay
                        if ii >= 0 and ii < m and jj >= 0 and jj < n and grid[ii][jj] == '1':
                            uf.union(i * n + j, ii * n + jj)
        return cnt + uf.query() - m * n

class UnionFind:
    def __init__(self, n):
        self.father = [i for i in xrange(n)]
        self.count = n
    def union(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b
            self.count -= 1
    def find(self, a):
        if a == self.father[a]:
            return a
        self.father[a] = self.find(self.father[a])
        return self.father[a]
    def query(self, ):
        return self.count
```



