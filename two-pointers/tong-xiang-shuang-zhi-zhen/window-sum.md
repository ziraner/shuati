Window Sum 题解

Given an array of n integer, and a moving window \(size k\), move the window at each iteration from the start of the array, find the`sum`of the element inside the window at each moving.

**Example**

For array`[1,2,7,8,5]`, moving window size k =`3`.  
1 + 2 + 7 = 10  
2 + 7 + 8 = 17  
7 + 8 + 5 = 20  
return`[10,17,20]`

Idea:

典型的sliding window题目

```
class Solution:
    # @param nums {int[]} a list of integers
    # @param k {int} size of window
    # @return {int[]} the sum of element inside the window at each moving
    def winSum(self, nums, k):
        # Write your code here
        n = len(nums)
        if k <= 0 or n < k:
            return []
        ans, pre_sum = [], 0
        for i in xrange(k):
            pre_sum += nums[i]
        ans.append(pre_sum)
        for j in xrange(i + 1, n):
            pre_sum += nums[j] - nums[j - k]
            ans.append(pre_sum)
        return ans
```



