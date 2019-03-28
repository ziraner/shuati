Maximum Subarray II

Given an array of integers, find two non-overlapping subarrays which have the largest sum.  
The number in each subarray should be contiguous.  
Return the largest sum.

##### Notice

The subarray should contain at least one number

**Example**

For given`[1, 3, -1, 2, -1, 2]`, the two subarrays are`[1, 3]`and`[2, -1, 2]`or`[1, 3, -1, 2]`and`[2]`, they both have the largest sum`7`.

Idea:

是maximum subarray的特殊情况，把1的结果从左向右保存在left里面，从右向左保存在right里面，然后遍历left right找最大

```
class Solution:
    """
    @param: nums: A list of integers
    @return: An integer denotes the sum of max two non-overlapping subarrays
    """
    def maxTwoSubArrays(self, nums):
        # write your code here
        # left[]: maximum subarray sum from the left
        # right[]: maximum subarray sum from the right
        n = len(nums)
        from sys import maxint
        left = [0 for _ in xrange(n)]
        right = [0 for _ in xrange(n)]
        preSum, minSum = 0, 0
        tmp = -maxint
        for i in xrange(n):
            preSum += nums[i]
            tmp = max(tmp, preSum - minSum)
            minSum = min(preSum, minSum)
            left[i] = tmp
        preSum, minSum = 0, 0
        tmp = -maxint
        for i in xrange(n - 1, -1, -1):
            preSum += nums[i]
            tmp = max(tmp, preSum - minSum)
            minSum = min(preSum, minSum)
            right[i] = tmp
        ans = -maxint
        for i in xrange(1, n):
            ans = max(ans, left[i - 1] + right[i])
        return ans
```



