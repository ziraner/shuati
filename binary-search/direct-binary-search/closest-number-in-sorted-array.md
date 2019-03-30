Closest Number in Sorted Array

**Problem:**

Given a target number and an integer array A sorted in ascending order, find the index `i` in A such that A\[i\] is closest to the given target. Return -1 if there is no element in the array.

**Example:**

Given`[1, 2, 3]`and target =`2`, return`1`.

Given`[1, 4, 6]`and target =`3`, return`1`.

Given`[1, 4, 6]`and target =`5`, return`1`or`2`.

Given`[1, 3, 3, 4]`and target =`2`, return`0`or`1`or`2`.

**Idea:**

Two possible ideas, find first position idx that is &gt;= target; Then compare idx - 1\(if available\) and idx.

**Solution:**

```python
class Solution:
    """
    @param A: an integer array sorted in ascending order
    @param target: An integer
    @return: an integer
    """
    def closestNumber(self, A, target):
        # write your code here
        idx = self.findFirstPosition(A, target)
        if idx == 0:
            return idx
        if target - A[idx - 1] < A[idx] - target:
            return idx - 1
        return idx

    # find first position that is >= target
    def findFirstPosition(self, A, target):
        start, end = 0, len(A) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] <= target:
                start = mid
            else:
                end = mid
        if A[start] >= target:
            return start
        return end
```

**Idea:**

Another possible solution is to find the last position that is <= target; Then compare idx and idx + 1\(if applicable\).

**Solution:**

```python
class Solution:
    """
    @param A: an integer array sorted in ascending order
    @param target: An integer
    @return: an integer
    """
    def closestNumber(self, A, target):
        # write your code here
        idx = self.findLastPosition(A, target)
        if idx == len(A) -1:
            return idx
        if A[idx + 1] - target < target - A[idx]:
            return idx + 1
        return idx

    # find last position that is <= target
    def findLastPosition(self, A, target):
        start, end = 0, len(A) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] <= target:
                start = mid
            else:
                end = mid
        if A[end] <= target:
            return end
        return start
```
