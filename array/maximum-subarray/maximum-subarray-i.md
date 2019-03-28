Maximum Subarray 解题报告

Find the contiguous subarray within an array \(containing at least one number\) which has the largest sum.

For example, given the array`[-2,1,-3,4,-1,2,1,-5,4]`,  
the contiguous subarray`[4,-1,2,1]`has the largest sum =`6`.

```
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        preSum, minSum = 0, 0
        from sys import maxint
        ans = -maxint
        for num in nums:
            preSum += num
            ans = max(ans, preSum - minSum)
            minSum = min(preSum, minSum)
        return ans
```



