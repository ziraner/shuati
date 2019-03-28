LintCode 457: Classical Binary Search 解题报告

Problem:

Find any position of a target number in a sorted array. Return -1 if target does not exist.

Idea:

if find target, return immediately

Solution:

```
class Solution:
    # @param {int[]} A an integer array sorted in ascending order
    # @param {int} target an integer
    # @return {int} an integer
    def findPosition(self, A, target):
        # Write your code here
        if not A:
            return -1
        n = len(A)
        start, end = 0, n - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] == target:
                return mid
            if A[mid] < target:
                start = mid
            else:
                end = mid
        if A[start] == target:
            return start
        if A[end] == target:
            return end
        return -1
```



