Lintcode 159: Find Minimum in Rotated Sorted Array 解题报告

Problem:

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

\(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).

Find the minimum element.

Notice

You may assume no duplicate exists in the array.

Example:

Given`[4, 5, 6, 7, 0, 1, 2]`return`0`

Idea:

Find the first X for OOOXXX

Solution:

Compare with the last number in the array: 记住就好了，跟第一个比有反例：12345

```
class Solution:
    # @param nums: a rotated sorted array
    # @return: the minimum number in the array
    def findMin(self, nums):
        # write your code here
        if not nums:
            return 0
        start, end = 0, len(nums) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if nums[mid] > nums[-1]:
                start = mid
            else:
                end = mid
        return min(nums[start], nums[end])
```



