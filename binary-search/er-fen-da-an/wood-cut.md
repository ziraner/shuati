Lintcode 183. Wood Cut 解题报告

Given n pieces of wood with length`L[i]`\(integer array\). Cut them into small pieces to guarantee you could have equal or more than k pieces with the same length. What is the longest length you can get from the n pieces of wood? Given L & k, return the maximum length of the small pieces.

##### Notice

You couldn't cut wood into float length.

If you couldn't get &gt;=_k_pieces, return`0`.

**Example**

For`L=[232, 124, 456]`,`k=7`, return`114`.

Idea:

二分答案

```
class Solution:
    """
    @param: L: Given n pieces of wood with length L[i]
    @param: k: An integer
    @return: The maximum length of the small pieces
    """
    def woodCut(self, L, k):
        # write your code here
        if L is None or len(L) == 0:
            return 0
        start, end = 1, max(L)
        while start + 1 < end:
            mid = (start + end) / 2
            if self.checkValid(L, k, mid):
                start = mid
            else:
                end = mid

        if self.checkValid(L, k, end):
            return end
        if self.checkValid(L, k, start):
            return start
        return 0

    def checkValid(self, L, k, length):
        count = 0
        for wood in L:
            count += wood / length
        if count >= k:
            return True
        else:
            return False

```

  


