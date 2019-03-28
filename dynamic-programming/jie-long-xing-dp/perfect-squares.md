Perfect Squares 解题报告

Given a positive integer`n`, find the least number of perfect square numbers \(for example,`1, 4, 9, 16, ...`\) which sum to n.

**Example**

Given n =`12`, return`3`because`12 = 4 + 4 + 4`  
Given n =`13`, return`2`because`13 = 4 + 9`

接龙型DP

f\[i\] = min\(所有可以通过加上一个平方数跳到i的数的f\[k\]\) + 1  
k = i - j \* j 遍历j从0到sqrt\(i\)

```
class Solution(object):
    def numSquares(self, n):
        """
        :type n: int
        :rtype: int
        """
        from sys import maxint
        from math import sqrt
        f = [maxint for _ in xrange(n + 1)]
        f[0] = 0
        f[1] = 1
        for i in xrange(1, n + 1):
            for j in xrange(1, int(sqrt(i)) + 1):
                f[i] = min(f[i - j * j] + 1, f[i])
        return f[n]
```



