Lintcode 462: Total Occurrence of Target 解题报告

Problem:

Given a target number and an integer array sorted in ascending order. Find the total number of occurrences of target in the array.

Example:

Given`[1, 3, 3, 4, 5]`and target =`3`, return`2`.

Given`[2, 2, 3, 4, 6]`and target =`4`, return`1`.

Given`[1, 2, 3, 4, 5]`and target =`6`, return`0`.

Idea:

Same to search range: find the first & last position of target in the sorted array.

Solution:

```
class Solution:
    # @param {int[]} A an integer array sorted in ascending order
    # @param {int} target an integer
    # @return {int} an integer
    def totalOccurrence(self, A, target):
        # Write your code here
        if not A: return 0
        n = len(A)
        start, end = 0, n - 1
        l, r = 0, 0
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] >= target:
                end = mid
            else:
                start = mid
        if A[start] == target:
            l = start
        elif A[end] == target:
            l = end
        else:
            return 0
        start, end = 0, n - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] > target:
                end = mid
            else:
                start = mid
        if A[end] == target:
            r = end
        else:
            r = start
        return r - l + 1
```



