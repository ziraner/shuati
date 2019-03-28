Unique Paths II解题报告

Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as`1`and`0`respectively in the grid.

##### Notice

mandnwill be at most 100.

**Example**

There is one obstacle in the middle of a 3x3 grid as illustrated below.

```
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]

```

The total number of unique paths is`2`.

思路：

DP跟I类似，加了个判断当前点是不是障碍物的选项，如果是的话则任何都走不到所以是0不是的话就是跟1一样了

```
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        f = [[0 for _ in xrange(n)] for _ in xrange(m)]
        f[0][0] = obstacleGrid[0][0] ^ 1
        for i in xrange(1, m):
            f[i][0] = (obstacleGrid[i][0] ^ 1) * f[i - 1][0]
        for j in xrange(1, n):
            f[0][j] = (obstacleGrid[0][j] ^ 1) * f[0][j - 1]
        for i in xrange(1, m):
            for j in xrange(1, n):
                if obstacleGrid[i][j] != 1:
                    f[i][j] = f[i - 1][j] + f[i][j - 1]
        return f[m - 1][n - 1]


```





