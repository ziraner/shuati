Climbing Stairs 解题报告

You are climbing a stair case. It takes **n** steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Example**

Given an example n=3 , 1+1+1=2+1=1+2=3

return 3

坐标型DP，跟斐波那契序列一样。

```
class Solution:
    """
    @param n: An integer
    @return: An integer
    """
    def climbStairs(self, n):
        # write your code here
        # O(n) space
        """
        if n < 0:
            return 0
        f = [1 for _ in range(n + 1)]
        for i in range(2, n + 1):
            f[i] = f[i - 1] + f[i - 2]
        return f[n]
        """
        # O(1) space
        if n <= 1:
            return 1
        prev = prev_prev = 1
        curt = 0
        for i in range(1, n):
            curt = prev + prev_prev
            prev_prev = prev
            prev = curt
        return curt

```

  
  


  




