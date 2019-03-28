Jump Game II解题报告

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

思路：

DP

```
from sys import maxint
class Solution:
    """
    @param: A: A list of integers
    @return: An integer
    """
    def jump(self, A):
        # write your code here
        # f[i]: minimal number of jumps to jump to i
        """
        if A is None:
            return 0
        n = len(A)
        f = [maxint for _ in range(n)]
        f[0] = 0
        for i in range(1, n):
            for j in range(0, i):
                if f[j] != maxint and j + A[j] >= i:
                    f[i] = min(f[i], f[j] + 1)
        return f[n - 1]
```



