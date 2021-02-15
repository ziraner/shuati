Number of Islands II 解题报告

A 2d grid map of`m`rows and`n`columns is initially filled with water. We may perform anaddLandoperation which turns the water at position \(row, col\) into a land. Given a list of positions to operate,**count the number of islands after eachaddLandoperation**. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.  
**Example:**

Given`m = 3, n = 3`,`positions = [[0,0], [0,1], [1,2], [2,1]]`.  
We return the result as an array:`[1, 1, 2, 3]`

Idea:

UnionFind，时间复杂度O\(n \* m\) + O\(4 \* k\)
用一个flag数组记录当前点是否被访问（即当前岛屿和海洋的status），用一个cnt变量记录当前一共加入了多少个岛屿（重复加入的不算）；在UnionFind中开一个变量cnt记录当前没有联通的数量

```python
class Solution(object):
    def numIslands2(self, m, n, positions):
        """
        :type m: int
        :type n: int
        :type positions: List[List[int]]
        :rtype: List[int]
        """
        uf = UnionFind(m * n)
        flag = [[False for _ in xrange(n)] for _ in xrange(m)]
        delta = [[0, 1], [0, -1], [1, 0], [-1, 0]]
        ans, cnt = [], 0
        for x, y in positions:
            if not flag[x][y]:
                flag[x][y] = True
                cnt += 1
                for deltax, deltay in delta:
                    xx, yy = x + deltax, y + deltay
                    if xx >= 0 and xx < m and yy >= 0 and yy < n and flag[xx][yy]:
                        uf.union(xx * n + yy , x * n + y)
            ans.append(cnt + uf.query() - m * n)
        return ans
class UnionFind:
    def __init__(self, n):
        self.father = [i for i in xrange(n)]
        self.count = n
    def find(self, a):
        if a == self.father[a]:
            return a
        self.father[a] = self.find(self.father[a])
        return self.father[a]
    def union(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b
            self.count -= 1
    def query(self, ):
        return self.count
```
