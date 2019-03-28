Lintcode 61: Search for a Range 解题报告

Problem:

Given a sorted array of\_n\_integers, find the starting and ending position of a given target value.

If the target is not found in the array, return`[-1, -1]`.

Example:

Given`[5, 7, 7, 8, 8, 10]`and target value`8`,  
return`[3, 4]`.

Idea:

Search Range: Search first & last Position in sorted array

Solution:

```
class Solution:
    """
    @param A : a list of integers
    @param target : an integer to be searched
    @return : a list of length 2, [index1, index2]
    """
    def searchRange(self, A, target):
        # write your code here
        if not A:
            return [-1, -1]
        n = len(A)
        start, end = 0, n - 1
        ans = []
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] >= target:
                end = mid
            else:
                start = mid
        if A[start] == target:
            ans.append(start)
        elif A[end] == target:
            ans.append(end)
        else:
            return [-1, -1]
        start, end = 0, n - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] > target:
                end = mid
            else:
                start = mid
        if A[end] == target:
            ans.append(end)
        else:
            ans.append(start)
        return ans
```



