Lintcode 75: Find Peak Element 解题报告

There is an integer array which has the following features:

* The numbers in adjacent positions are different.
* A\[0\] &lt; A\[1\] & A\[A.length - 2\] &gt; A\[A.length - 1\].

We define a position P is a peek if:

```
A[P] > A[P-1] && A[P] > A[P+1]
```

Find a peak element in this array. Return the index of the peak.

##### Notice

* It's guaranteed the array has at least one peak.
* The array may contain multiple peeks, find any of them.
* The array has at least 3 numbers in it.

**Example**

Given`[1, 2, 1, 3, 4, 5, 7, 6]`

Return index`1`\(which is number 2\) or`6`\(which is number 7\)

Idea:

Find any X in a lot of OOOXOOO

```
class Solution:
    #@param A: An integers list.
    #@return: return any of peek positions.
    def findPeak(self, A):
        # write your code here
        start, end = 1, len(A) - 2
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] < A[mid - 1]:
                end = mid
            else:
                start = mid
        if A[start] >= A[end]:
            return start
        return end
```



