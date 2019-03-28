Maximal Rectangle 解题报告

Given a 2D`boolean`matrix filled with`False`and`True`, find the largest rectangle containing all`True`and return its area.

**Example**

Given a matrix:

```
[
  [1, 1, 0, 0, 1],
  [0, 1, 0, 0, 1],
  [0, 0, 1, 1, 1],
  [0, 0, 1, 1, 1],
  [0, 0, 0, 0, 1]
]
```

return`6`.

Idea:

这个题乍一看是Maximal Square的特殊情况，可以用DP解但是想一想要找长和宽所以保守估计应该是O\(n^3\)的时间复杂度。  
这个复杂度有些过高了，利用单调栈的特性可以将这个题处理为Largest Rectangle in Histogram的特殊情况。

对每一行而言如果matrix\[i\]\[j\]是0则为0；否则为上一行的值加上这一行的值  
对每一行的值做Largest Rectangle in Histogram，并一直保存更新最大面积

```
class Solution(object):
    def maximalRectangle(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        if not matrix or not matrix[0]:
            return 0
        m, n = len(matrix), len(matrix[0])
        rec = [-1 for _ in xrange(n + 1)]
        ans = 0
        for i in xrange(m):
            for j in xrange(n):
                if i == 0:
                    if matrix[i][j] == '1':
                        rec[j] = 1
                    else:
                        rec[j] = 0
                else:
                    if matrix[i][j] == '1':
                        rec[j] += 1
                    else:
                        rec[j] = 0
            stack = []
            for i in xrange(n + 1):
                while stack and rec[i] < rec[stack[-1]]:
                    h = rec[stack.pop()]
                    if stack:
                        w = i - stack[-1] - 1
                    else:
                        w = i
                    ans = max(ans, w * h)
                stack.append(i)
        return ans
```



