House Robber解题报告

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and**it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight**without alerting the police**.

Given`[3, 8, 4]`, return`8`.

思路

f\[i\] 表示前i个房子中，偷到的最大价值  
f\[i\] = max\(f\[i-1\], f\[i-2\] + A\[i-1\]\)

可以使用滚动优化

```
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        n = len(nums)
        f = [0 for _ in xrange(n + 1)]
        f[1] = nums[0]
        for i in xrange(2, n + 1):
            f[i] = max(nums[i - 1] + f[i - 2], f[i - 1])
        return f[n]
```

优化之后

```
class Solution:
    """
    @param: A: An array of non-negative integers
    @return: The maximum amount of money you can rob tonight
    """
    def houseRobber(self, A):
        # write your code here
        # f[i]: maximum amount of money robbed from 0 to i
        if not A:
            return 0
        n = len(A)
        f = [0 for _ in range(2)]
        f[0] = 0
        f[1] = A[0]
        for i in range(2, n + 1):
            f[i % 2] = max(f[(i - 1) % 2], f[i % 2] + A[i - 1])
        return f[n % 2]
```



