Lintcode 390: Find Peak Element II 解题报告

There is an integer matrix which has the following features:

* The numbers in adjacent positions are different.
* The matrix has n rows and m columns.
* For all i &lt; m, _A\[0\]\[i\] &lt; A\[1\]\[i\] && A\[n - 2\]\[i\] &gt; A\[n - 1\]\[i\]_
* For all j &lt; n, _A\[j\]\[0\] &lt; A\[j\]\[1\] && A\[j\]\[m - 2\] &gt; A\[j\]\[m - 1\]_

We define a position P is a peek if:

```
A[j][i] > A[j+1][i] && A[j][i] > A[j-1][i] && A[j][i] > A[j][i+1] && A[j][i] > A[j][i-1]
```

Find a peak element in this matrix. Return the index of the peak.

##### Notice

The matrix may contains multiple peeks, find any of them.

**Example**

Given a matrix:

```
[
  [1 ,2 ,3 ,6 ,5],
  [16,41,23,22,6],
  [15,17,24,21,7],
  [14,18,19,20,10],
  [13,14,11,10,9]
]
```

return index of 41 \(which is`[1,1]`\) or index of 24 \(which is`[2,2]`\)

Idea:

这个题目不是基本的二分法，但是是二分法的思想。

对行来说：每次取中点，找该中点行中最大值，标记为A\[mid\]\[max\]。如果A\[mid\]\[max\] &lt; A\[mid - 1\]\[max\]则peak一定在行start, mid - 1中；如果A\[mid\]\[max\] &lt; A\[mid + 1\]\[max\]则最大值一定在mid + 1, end中；如果这个点比A\[mid - 1\]\[max\], A\[mid + 1\]\[max\]都大则找到解直接返回。同理，对列进行同样操作。alternate行和列：在递归函数中写一个cnt，每次cnt + 1

时间复杂度分析：通过O\(m + n\)的时间将T\(mn\)的问题变成了T\(1/4\*m\*n\)的问题，则时间复杂度是O\(m + n\)

```
class Solution:
    """
    @param: A: An integer matrix
    @return: The index of the peak
    """
    def findPeakII(self, A):
        # write your code here
        return self.helper(A, 0, 1, len(A[0]) - 2, 1, len(A) - 2)
    def helper(self, A, cnt, left, right, upper, bottom):
        if cnt % 2 == 0:
            mid = (upper + bottom) / 2
            idx = left
            for j in xrange(left + 1, right + 1):
                if A[mid][idx] < A[mid][j]:
                    idx = j
            if A[mid][idx] < A[mid - 1][idx]:
                return self.helper(A, cnt + 1, left, right, upper, mid - 1)
            elif A[mid][idx] < A[mid + 1][idx]:
                return self.helper(A, cnt + 1, left, right, mid + 1, bottom)
            else:
                return [mid, idx]
        else:
            mid = (left + right) / 2
            idx = upper
            for i in xrange(upper + 1, bottom + 1):
                if A[idx][mid] < A[i][mid]:
                    idx = i
            if A[idx][mid] < A[idx][mid - 1]:
                return self.helper(A, cnt + 1, left, mid - 1, upper, bottom)
            elif A[idx][mid] < A[idx][mid + 1]:
                return self.helper(A, cnt + 1, mid + 1, right, upper, bottom)
            else:
                return [idx, mid]
```



