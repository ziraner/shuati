Maximal Square 解题报告

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing all 1's and return its area.

**Example**

For example, given the following matrix:

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```

Return`4`.

Idea:

1. 状态 State

f\[i\]\[j\] 表示以i和j作为正方形右下角可以拓展的最大边长

2. 方程 Function

if matrix\[i\]\[j\] == 1     f\[i\]\[j\] = min\(f\[i - 1\]\[j\], f\[i\]\[j-1\], f\[i-1\]\[j-1\]\) + 1;

if matrix\[i\]\[j\] == 0     f\[i\]\[j\] = 0

3. 初始化 Intialization f\[i\]\[0\] = matrix\[i\]\[0\]; f\[0\]\[j\] = matrix\[0\]\[j\];

4. 答案 Answer max{f\[i\]\[j\]}

```
class Solution(object):
    def maximalSquare(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        if not matrix or not matrix[0]:
            return 0
        m, n = len(matrix), len(matrix[0])
        f = [[0 for _ in xrange(n)] for _ in xrange(m)]
        ans = 0
        for i in xrange(m):
            if matrix[i][0] == '1':
                f[i][0] = 1
                ans = 1
        for j in xrange(n):
            if matrix[0][j] == '1':
                f[0][j] = 1
                ans = 1
        for i in xrange(1, m):
            for j in xrange(1, n):
                if matrix[i][j] == '1':
                    f[i][j] = min(f[i - 1][j - 1], f[i][j - 1], f[i - 1][j]) + 1
                    ans = max(ans, f[i][j])
        return ans * ans
```

滚动数组优化空间

```
class Solution(object):
    def maximalSquare(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        if not matrix or not matrix[0]:
            return 0
        m, n = len(matrix), len(matrix[0])
        ans = 0
        f = [[0 for _ in xrange(n)] for _ in xrange(2)]
        for i in xrange(m):
            if matrix[i][0] == '1':
                f[i % 2][0] = 1
            else:
                f[i % 2][0] = 0
            ans = max(ans, f[i % 2][0])
            for j in xrange(1, n):
                if i == 0:
                    if matrix[i][j] == '1':
                        f[i][j] = 1
                else:
                    if matrix[i][j] == '1':
                        f[i % 2][j] = min(f[i % 2][j - 1], f[(i - 1) % 2][j], f[(i - 1) % 2][j - 1]) + 1
                    else:
                        f[i % 2][j] = 0
                ans = max(ans, f[i % 2][j])
        return ans * ans
```



