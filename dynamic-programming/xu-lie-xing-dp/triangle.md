Triangle解题报告

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

##### Notice

Bonus point if you are able to do this using only O\(n\) extra space, where n is the total number of rows in the triangle.

**Example**

Given the following triangle:

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is 11 \(i.e., 2 + 3 + 5 + 1 = 11\).

Idea

坐标型DP，初始化第一行和第一列，这里还要初始化对角线上的点。  
函数f\[i\]\[j\]表示到i,j的地方的最小的path sum  
最后可以用滚动数组优化

```
class Solution:
    def minimumTotal(self, triangle):
        if triangle is None or triangle[0] is None:
            return 0
        n = len(triangle)
        m = len(triangle[n - 1])
        # f[i][j]: dao dang qian dian i, j de zui xiao total
        f = [[maxint for _ in range(n)] for _ in range(m)]
        # initialization
        f[0][0] = triangle[0][0]
        for i in range(1, n):
            f[i][0] = f[i - 1][0] + triangle[i][0]
            f[i][i] = f[i - 1][i - 1] + triangle[i][i]
        # function
        for i in range(1, n):
            for j in range(1, i):
                f[i][j] = min(f[i - 1][j - 1], f[i - 1][j]) + triangle[i][j]
        # answer
        return min(f[n - 1])
```



