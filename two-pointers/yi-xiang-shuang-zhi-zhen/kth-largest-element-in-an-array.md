Kth Largest Element in an Array 解题报告

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.
For example, Given`[3,2,1,5,6,4]`and k = 2, return 5.

**Note:**
>You may assume k is always valid, 1 ≤ k ≤ array's length.

**Idea**
>这个题目典型的quick select 时间复杂度O\(n\)

```python
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        return self.quickSelect(nums, k, 0, len(nums) - 1)
    def quickSelect(self, nums, k, start, end):
        if start >= end:
            return nums[start]
        left, right = start, end
        pivot = nums[(start + end) / 2]
        while left <= right:
            while left <= right and nums[left] > pivot:
                left += 1
            while left <= right and nums[right] < pivot:
                right -= 1
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        if start + k - 1 <= right:
            return self.quickSelect(nums, k, start, right)
        if start + k - 1 >= left:
            return self.quickSelect(nums, k - (left - start), left, end)
        return nums[right + 1]
```
