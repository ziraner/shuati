Lintcode 633: Find the Duplicate Number 解题报告

Given an array nums containing n+ 1 integers where each integer is between 1 and n\(inclusive\), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

**Note:**

1. You **must not **modify the array \(assume the array is read only\).
2. You must use only constant, O\(1\) extra space.
3. Your runtime complexity should be less than`O(n^2)`
4. There is only one duplicate number in the array, but it could be repeated more than once.

**Example**

Given`nums`=`[5,5,4,3,2,1]`return`5`  
Given`nums`=`[5,4,4,3,2,1]`return`4`

Idea:

对数组进行二分，每次二分后查比其小的数的数目，如果是小于等于当前数的话则说明这里面没有数多余，一定在另外一半答案中。

Solution:

```
class Solution:
    """
    @param: nums: an array containing n + 1 integers which is between 1 and n
    @return: the duplicate one
    """
    def findDuplicate(self, nums):
        # write your code here
        start, end = 1, len(nums)
        while start + 1 < end:
            mid = (start + end) / 2
            if self.check(mid, nums):
                start = mid
            else:
                end = mid
        if self.check(start, nums):
            return end
        return start
    def check(self, val, nums):
        count = 0
        for i in range(len(nums)):
            if nums[i] <= val:
                count += 1
        return count <= val
```



