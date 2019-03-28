Kth Smallest Sum In Two Sorted Arrays 解题报告

Given two integer arrays sorted in ascending order and an integer k. Define_sum = a + b_, where_a_is an element from the first array and_b_is an element from the second one. Find the_k_th smallest sum out of all possible sums.

**Example**

Given`[1, 7, 11]`and`[2, 4, 6]`.

For k =`3`, return`7`.

For k =`4`, return`9`.

For k =`8`, return`15`.

Idea:

乍一看这个题目最小的一定是\(0, 0\)，然后是\(1, 0\)或者\(0, 1\)，然后是\(1, 0\), \(0, 1\), \(2, 0\), \(1, 1\), \(0, 2\)中的四个...是一个越来越多的过程，貌似没什么思路。但是仔细想想，我们需要一个heap来保存这些点且找到谁是最小的然后从这个最小的去扩展，所以这个题目可以扩展为以heap为queue，以两个1维array为“矩阵”的BFS，delta = \[\[0, 1\], \[1, 0\]\]这里delta为两个数组中坐标的增量

```
from heapq import heappush, heappop
class Solution:
    
    """
    @param: A: an integer arrays sorted in ascending order
    @param: B: an integer arrays sorted in ascending order
    @param: k: An integer
    @return: An integer
    """
    def kthSmallestSum(self, A, B, k):
        # write your code here
        if not A or not B:
            return 0
        m, n = len(A), len(B)
        visited = [[False for _ in xrange(n)] for _ in xrange(m)]
        hq = []
        heappush(hq, (A[0] + B[0], 0, 0))
        visited[0][0] = True
        rank = 1
        while hq:
            val, x, y = heappop(hq)
            if rank == k:
                return val
            for deltax, deltay in [[1, 0], [0, 1]]:
                xx, yy = x + deltax, y + deltay
                if xx < m and yy < n and not visited[xx][yy]:
                    heappush(hq, (A[xx] + B[yy], xx, yy))
                    visited[xx][yy] = True
            rank += 1
        return 0
```



