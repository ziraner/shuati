Lintcode 617: Maximum Average Subarray 解题报告

Problem:

Given an array with positive and negative numbers, find the`maximum average subarray`which length should be greater or equal to given length`k`.

##### Notice

It's guaranteed that the size of the array is greater or equal to _k_.

**Example**

Given nums =`[1, 12, -5, -6, 50, 3]`, k =`3`

Return`15.667`// \(-6 + 50 + 3\) / 3 = 15.667

Idea:

二分答案，对min和max number中做二分法，每一个avg value去判断是否是可行解。  
可行解判断：判断是否存在一个subarray，使得平均和大于等于当前可行解，转化为先将原来数组每个值都减去可行解，然后是否存在length &gt;= k的subarray使得subarray和大于等于0，一道经典的subarray sum问题

Solution:

```
from sys import maxint

class Solution:
    # @param {int[]} nums an array with positive and negative numbers
    # @param {int} k an integer
    # @return {double} the maximum average
    def maxAverage(self, nums, k):
        # Write your code here
        start, end = min(nums), max(nums)
        error = 1e-6
        while start + error < end:
            mid = (start + end) / 2.0
            if self.check(mid, nums, k):
                start = mid
            else:
                end = mid
        return start
    # this is similar to maximum subarray IV
    def check(self, ans, nums, k):
        min_pre = 0
        n = len(nums)
        preSum = [0 for _ in range(n + 1)]
        for i in range(1, n + 1):
            preSum[i] = nums[i - 1] + preSum[i - 1] - ans
            if i >= k and preSum[i] - min_pre >= 0: 
                return True
            if i >= k:
                min_pre = min(min_pre, preSum[i - k + 1])
        return False
        
```



