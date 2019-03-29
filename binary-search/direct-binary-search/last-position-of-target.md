LintCode 458: Last Position of Target

**Problem:**

Find the last position of a target number in a sorted array. Return -1 if target does not exist.

**Idea:**

Opposite to First Position:

Last Position of a target number: combine A\[mid\] == target and A\[mid\] &lt; target;

Solution:

```python
class Solution:
    # @param {int[]} A an integer array sorted in ascending order
    # @param {int} target an integer
    # @return {int} an integer
    def lastPosition(self, A, target):
        # Write your code here
        if not A:
            return -1
        start, end = 0, len(A) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] > target:
                end = mid
            else:
                start = mid
        if A[end] == target:
            return end
        if A[start] == target:
            return start
        return -1
```
