Lintcode 585: Maximum Number in Mountain Sequence 解题报告

Problem:

Given a mountain sequence of`n`integers which increase firstly and then decrease, find the mountain top.

Example:

Given`nums`=`[1, 2, 4, 8, 6, 3]`return`8`  
Given`nums`=`[10, 9, 8, 7]`, return`10`

Idea:

Similar to Find Peak: Find X in OOOXOOO  
Solution:

```
class Solution:
    # @param {int[]} nums a mountain sequence which increase firstly and then decrease
    # @return {int} then mountain top
    def mountainSequence(self, nums):
        # Write your code here
        if not nums:
            return 0
        start, end = 0, len(nums) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if nums[mid] < nums[mid - 1]:
                end = mid
            else:
                start = mid
        return max(nums[start], nums[end])
```



