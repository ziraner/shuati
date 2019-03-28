LintCode 460: Find K Closest Elements 解题报告

Problem:

Given a target number, a non-negative integer`k`and an integer array A sorted in ascending order, find the k closest numbers to target in A, sorted in ascending order by the difference between the number and target. Otherwise, sorted in ascending order by number if the difference is same.

Example:

Given A =`[1, 2, 3]`, target =`2`and k =`3`, return`[2, 1, 3]`.

Given A =`[1, 4, 6, 8]`, target =`3`and k =`3`, return`[4, 1, 6]`.

Idea:

Similar to Closest Number in Sorted Array, define a left bound and right bound to cover the whole k.

Be careful with corner case: len\(A\) &lt;k

```
class Solution:
    # @param {int[]} A an integer array
    # @param {int} target an integer
    # @param {int} k a non-negative integer
    # @return {int[]} an integer array

    def kClosestNumbers(self, A, target, k):
        # Write your code here
        n = len(A)
        if n < k:
            return A
        idx = self.firstPosition(A, target)
        l, r = idx - 1, idx
        ans = []
        while True:
            if len(ans) == k:
                break
            if l >= 0 and r < n and abs(A[l] - target) < abs(A[r] - target):
                ans.append(A[l])
                l -= 1
            elif l >= 0 and r < n and abs(A[l] - target) > abs(A[r] - target):
                ans.append(A[r])
                r += 1
            elif l >= 0:
                ans.append(A[l])
                l -= 1
            else:
                ans.append(A[r])
                r += 1
        return ans
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



