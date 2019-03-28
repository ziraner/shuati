Unique Paths解题报告

A robot is located at the top-left corner of a\_m\_x\_n\_grid.

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid.

How many possible unique paths are there?

##### Notice

\_m\_and\_n\_will be at most 100.

**Example**

Given m =`3`and n =`3`, return`6`.  
Given m =`4`and n =`5`, return`35`.

Idea

坐标型DP  
f\[i\]\[j\]为到i,j共有多少种不同的方式

```
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        f = [[1 for _ in xrange(n)] for _ in xrange(m)]
        for i in xrange(1, m):
            for j in xrange(1, n):
                f[i][j] = f[i - 1][j] + f[i][j - 1]
        return f[m - 1][n - 1]
```

这个题目需要想明白的一个点是，如果四个方向都能走，一般来说不能用dp因为存在着循环依赖关系。但是滑雪问题除外，即Longest Increasing Continuous subsequence II，因为存在着一个数值上下降或者上升的趋势，所以还是可以DP

