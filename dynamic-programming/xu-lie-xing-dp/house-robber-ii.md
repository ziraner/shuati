House Robber II解题报告

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are**arranged in a circle**. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight**without alerting the police**.

**Example**

nums =`[3,6,4]`, return`6`

思路：

因为环绕起来了，所以对小偷来说，对于房子0，要么偷要么不偷：偷的话就不能偷n - 1，所以偷的范围是0~n-2；不偷的话就可以偷1~n-1，算两次判断最大值就OK

```
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        if n == 0:
            return 0
        if n == 1:
            return nums[0]
        return max(self.rob1(0, n - 2, nums), self.rob1(1, n - 1, nums))
    def rob1(self, start, end, nums):
        f = [0, 0]
        for i in xrange(start, end + 1):
            f[i % 2] = max(f[i % 2] + nums[i], f[(i - 1) % 2])
        return f[end % 2]
```



