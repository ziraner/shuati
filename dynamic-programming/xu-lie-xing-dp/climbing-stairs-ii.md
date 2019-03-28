Climbing Stairs II 解题报告

A child is running up a staircase with`n`steps, and can hop either 1 step, 2 steps, or 3 steps at a time. Implement a method to count how many possible ways the child can run up the stairs.

思路：

function: f\[i\] = f\[i - 1\] + f\[i - 2\] + f\[i - 3\]

```
class Solution:
    """
    @param {int} n a integer
    @return {int} a integer
    """
    def climbStairs2(self, n):
        # Write your code here
        if n <= 1:
            return 1
        f = [1 for _ in range(n + 1)]
        f[2] = 2
        for i in range(3, n + 1):
            f[i] = f[i - 3] + f[i - 2] + f[i - 1]
        return f[n]
```



