Closest Number in Sorted Array

**Problem:**

Given a target number and an integer array A sorted in ascending order, find the index `i` in A such that A\[i\] is closest to the given target. Return -1 if there is no element in the array.

**Example:**

Given`[1, 2, 3]`and target =`2`, return`1`.

Given`[1, 4, 6]`and target =`3`, return`1`.

Given`[1, 4, 6]`and target =`5`, return`1`or`2`.

Given`[1, 3, 3, 4]`and target =`2`, return`0`or`1`or`2`.

**Idea:**

Similar to insert position, find first position idx that is &gt;= target; Then compare idx - 1\(if available\) with idx. Corner Case: idx == 0, idx == n

Solution:

```python
class Solution:
    # @param {int[]} A an integer array sorted in ascending order
    # @param {int} target an integer
    # @return {int} an integer
    def closestNumber(self, A, target):
        # Write your code here
        if not A:
            return -1
        n = len(A)
        idx = self.firstPosition(A, target)
        if idx == 0:
            return 0
        if idx == n:
            return n - 1
        if target - A[idx - 1] <= A[idx] - target:
            return idx - 1
        return idx
    def firstPosition(self, A, target):
        n = len(A)
        start, end = 0, n - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] >= target:
                end = mid
            else:
                start = mid
        if A[start] >= target:
            return start
        if A[end] >= target:
            return end
        return end + 1
```
