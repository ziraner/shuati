Merge k Sorted Arrays解题报告

Given\_k\_sorted integer arrays, merge them into one sorted array.  
**Example**

Given 3 sorted arrays:

```
[
  [1, 3, 5, 7],
  [2, 4, 6],
  [0, 8, 9, 10, 11]
]
```

return`[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]`.

idea

非常经典的k路归并问题。两种方法，divide & conquer和heapq

方法一： heap

```
from heapq import heappush, heappop
class Solution:
    # @param {int[][]} arrays k sorted integer arrays
    # @return {int[]} a sorted array
    def mergekSortedArrays(self, arrays):
        # Write your code here
        # heap
        h, ans = [], []
        for i in xrange(len(arrays)):
            if arrays[i]:
                heappush(h, (arrays[i][0], i, 0))
        while h:
            val, x, y = heappop(h)
            if y + 1 < len(arrays[x]):
                heappush(h, (arrays[x][y + 1], x, y + 1))
            ans.append(val)
        return ans
```

方法二：mergesort的思想：divide and conquer

```
from heapq import heappush, heappop
class Solution:
    # @param {int[][]} arrays k sorted integer arrays
    # @return {int[]} a sorted array
    def mergekSortedArrays(self, arrays):
        # Write your code here
        # divide and conquer
        """
        n = len(arrays)
        if n == 0:
            return []
        if n == 1:
            return arrays[0]
        left = self.mergekSortedArrays(arrays[: n / 2])
        right = self.mergekSortedArrays(arrays[n / 2 :])
        if left and right:
            return self.merge(left, right)
        if left:
            return left
        if right:
            return right
        return []
    def merge(self, l1, l2):
        m, n = len(l1), len(l2)
        i, j = 0, 0
        result = []
        while i < m and j < n:
            if l1[i] < l2[j]:
                result.append(l1[i])
                i += 1
            else:
                result.append(l2[j])
                j += 1
        if i < m:
            result += l1[i:]
        if j < n:
            result += l2[j:]
        return result
        """
```



