Lintcode 586: Sqr\(x\) II 解题报告

Implement`double sqrt(double x)`and`x >= 0`.

Compute and return the square root of x.

##### Notice

You do not care about the accuracy of the result, we will help you to output results.

**Example**

Given`n`=`2`return`1.41421356`

Idea:

在普通的二分法中，循环是while start + 1 &lt; end，而在这个二分法中，while start + error &lt; end

Solution:

```
class Solution:
    # @param {double} x a double
    # @return {double} the square root of x
    def sqrt(self, x):
        # Write your code here
        error = 1e-12
        start = 0 * 1.0
        if x < 1:
            end = 1.0
        else:
            end = x * 1.0
        while start + error < end:
            mid = (start + end) / 2
            if mid * mid < x:
                start = mid
            else:
                end = mid
        return end
```



