Minimum Path Sum解题报告

Given a **m x n** grid filled with non-negative numbers, find a path from top left to bottom right which **minimizes** the sum of all numbers along its path.

##### Notice

You can only move either down or right at any point in time.

Idea

坐标型dp

f\[i\]\[j\]表示到\(i, j\)的时候最小的path sum  
初始化第一行第一列

可以滚动数组优化

```
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        if not grid or not grid[0]:
            return 0
        m, n = len(grid), len(grid[0])
        f = [[0 for _ in xrange(n)] for _ in xrange(m)]
        f[0][0] = grid[0][0]
        for i in xrange(1, m):
            f[i][0] = grid[i][0] + f[i - 1][0]
        for j in xrange(1, n):
            f[0][j] = grid[0][j] + f[0][j - 1]
        for i in xrange(1, m):
            for j in xrange(1, n):
                f[i][j] = min(f[i - 1][j], f[i][j - 1]) + grid[i][j]
        return f[m - 1][n - 1]
```



