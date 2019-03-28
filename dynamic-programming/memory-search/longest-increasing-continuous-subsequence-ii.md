Longest Increasing Continuous subsequence II解题报告

Give you an integer matrix \(with row size n, column size m\)，find the longest increasing continuous subsequence in this matrix. \(The definition of the longest increasing continuous subsequence here can start at any row or column and go up/down/right/left any direction\).  
**Example**

Given a matrix:

```
[
  [1 ,2 ,3 ,4 ,5],
  [16,17,24,23,6],
  [15,18,25,22,7],
  [14,19,20,21,8],
  [13,12,11,10,9]
]
```

return`25`

这是一道memorizationsearch的最经典问题，相对于这个题目的变种题目有滑雪问题：有一个二维矩阵，是坡的高度，问咋滑能滑到最长的长度的雪。

最基本的想法是DFS做。但是要对每一个点都做一次DFS，时间复杂度贼高O\(n^2\*m^2\)。其实搜索的过程中是可以记忆化的。

记忆化搜索：因为我们不知道咋初始化，起点在哪儿很烦找不到，且状态转移基本懵逼，可以上下左右四个方向转移，一般的DP loop解决不了的，所以要用记忆化搜索来做。

```
from sys import maxint
class Solution:
    def longestIncreasingContinuousSubsequenceII(self, A):
        if not A or not A[0]:
            return 0
        m, n = len(A), len(A[0])
        dp = [[1 for _ in xrange(n)] for _ in xrange(m)]
        flag = [[False for _ in xrange(n)] for _ in xrange(m)]
        ans = 1
        for i in xrange(m):
            for j in xrange(n):
                ans = max(ans, self.msearch(dp, flag, A, i, j))
        return ans
    def msearch(self, dp, flag, A, i, j):
        if flag[i][j]:
            return dp[i][j]
        flag[i][j] = True
        m, n = len(A), len(A[0])
        delta = [[0, 1], [0, -1], [1, 0], [-1, 0]]
        for deltax, deltay in delta:
            ii, jj = deltax + i, deltay + j
            if ii < 0 or ii >= m or jj < 0 or jj >= n:
                continue
            if A[ii][jj] < A[i][j]:
                dp[i][j] = max(dp[i][j], self.msearch(dp, flag, A, ii, jj) + 1)
        return dp[i][j]
```



