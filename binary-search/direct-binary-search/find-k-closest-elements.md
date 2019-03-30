Find K Closest Elements

**Problem:**

Given a target number, a non-negative integer `k` and an integer array A sorted in ascending order, find the k closest numbers to target in A, sorted in ascending order by the difference between the number and target. Otherwise, sorted in ascending order by number if the difference is same.

**Example:**

Given A =`[1, 2, 3]`, target =`2`and k =`3`, return`[2, 1, 3]`.

Given A =`[1, 4, 6, 8]`, target =`3`and k =`3`, return`[4, 1, 6]`.

**Idea:**

进阶版Closest Number in Sorted Array。找到closest之后用中心扩展法，用两个指针从中心点向左向右扩展直到找到k个数为止。

```python
class Solution:
    """
    @param A: an integer array
    @param target: An integer
    @param k: An integer
    @return: an integer array
    """
    def kClosestNumbers(self, A, target, k):
        # write your code here
        ans = []
        idx = self.findFirstPosition(A, target)
        left, right = idx - 1, idx
        while True:
            if len(ans) == k:
                break
            if left >= 0 and right < len(A):
                if target - A[left] <= A[right] - target:
                    ans.append(A[left])
                    left -= 1
                else:
                    ans.append(A[right])
                    right += 1
            elif left >= 0:
                ans.append(A[left])
                left -= 1
            else:
                ans.append(A[right])
                right += 1
        return ans

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
