Remove Duplicates from Sorted Array 解题报告

Given a sorted array, remove the duplicates[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm)such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by**modifying the input array**[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm)with O\(1\) extra memory.

**Example:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of 
nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.

```

idea:
remove duplicate numbers in array的排序数组情况同向双指针情况，时间复杂度O(n)

```
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        i, j = 0, 1
        while j < len(nums):
            if nums[i] != nums[j]:
                i += 1
                nums[i] = nums[j]
            j += 1
        return i + 1
                
```



  


