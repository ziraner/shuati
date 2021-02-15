Lintcode 14: First Position of Target

**Problem:**

For a given sorted array \(ascending order\) and a `target` number, find the first index of this number in `O(log n)` time complexity.

If the target number does not exist in the array, return`-1`.

**Idea:**

First Position of a target number: combine A\[mid\] == target and A\[mid\] &gt; target;

Solution:

```python
class Solution:
    # @param nums: The integer array
    # @param target: Target number to find
    # @return the first position of target in nums, position start from 0
    def binarySearch(self, nums, target):
        # write your code here
        if not nums:
            return -1
        start, end = 0, len(nums) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if nums[mid] >= target:
                end = mid
            else:
                start = mid
        if nums[start] == target:
            return start
        if nums[end] == target:
            return end
        return -1
```
