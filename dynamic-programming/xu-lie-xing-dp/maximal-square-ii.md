Maximal Square II 解题报告

Given a 2D binary matrix filled with`0`'s and`1`'s, find the largest square which diagonal is all`1`and others is`0`.

Notice

Only consider the main diagonal situation.

**Example**

For example, given the following matrix:

```
1 0 1 0 0
1 0 0 1 0
1 1 0 0 1
1 0 0 1 0
```

Return`9`

思路

除了原dp数组之外需要另外维护up和left两个数组，表示到i,j为止形成的up小长矩形和left小长矩形连续是0的个数。

```
class Solution:
    """
    @param: matrix: a matrix of 0 an 1
    @return: an integer
    """
    def maxSquare2(self, matrix):
        # write your code here
        if not matrix or not matrix[0]:
            return 0
        m, n = len(matrix), len(matrix[0])
        dp = [[0 for _ in range(n)] for _ in range(m)]
        up = [[0 for _ in range(n)] for _ in range(m)]
        lf = [[0 for _ in range(n)] for _ in range(m)]
        ans = 0
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == 0:
                    up[i][j], lf[i][j] = 1, 1
                    if i > 0:
                        up[i][j] = up[i - 1][j] + 1
                    if j > 0:
                        lf[i][j] = lf[i][j - 1] + 1
                else:
                    if i > 0 and j > 0:
                        dp[i][j] = min(dp[i - 1][j - 1], up[i - 1][j], lf[i][j - 1]) + 1
                    else:
                        dp[i][j] = 1
                ans = max(ans, dp[i][j])
        return ans * ans
```



