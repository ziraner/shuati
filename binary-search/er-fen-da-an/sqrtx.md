Lintcode 141: Sqrt\(x\) 解题报告

Implement`int sqrt(int x)`.

Compute and return the square root of x.

**x **is guaranteed to be a non-negative integer.

**Example 1:**

Input 4: Output: 2

Idea:

二分答案，error为1因为求整数

Solution:

```
class Solution(object):
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        if x == 0 or x == 1:
            return x
        start, end = 1, x
        while start + 1 < end:
            mid = (start + end) / 2
            if mid * mid == x:
                return mid
            elif mid * mid < x:
                start = mid
            else:
                end = mid
        if end * end <= x:
            return end
        return start
```



