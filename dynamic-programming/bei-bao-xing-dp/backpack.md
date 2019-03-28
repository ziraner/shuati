Bacpack 解题报告

Given_n_items with size Ai, an integer_m_denotes the size of a backpack. How full you can fill this backpack?

##### Notice

You can not divide any item into small pieces.

**Example**

If we have`4`items with size`[2, 3, 5, 7]`, the backpack size is 11, we can select`[2, 3, 5]`, so that the max size we can fill this backpack is`10`. If the backpack size is`12`. we can select`[2, 3, 7]`so that we can fulfill the backpack.

You function should return the max size we can fill in the given backpack.

背包类DP

f\[i\]\[S\] “前i”个物品，取出一些能否组成和为S

f\[i\]\[S\] = f\[i-1\]\[S - a\[i-1\]\] or f\[i-1\]\[S\]  a\[i-1\] 是第i个物品下标是i-1

f\[i\]\[0\] = true; f\[0\]\[1..target\] = false

检查所有的f\[n\]\[j\]

O\(n\*S\) ， 滚动数组优化

```
class Solution:
    # @param m: An integer m denotes the size of a backpack
    # @param A: Given n items with size A[i]
    # @return: The maximum size
    def backPack(self, m, A):
        # write your code here
        if not A:
            return 0
        n = len(A)
        f = [[False for _ in range(m + 1)] for _ in range(2)]
        f[0][0] = True
        for i in xrange(1, n + 1):
            f[i % 2][0] = True
            for j in xrange(1, m + 1):
                if j >= A[i - 1]:
                    f[i % 2][j] = f[(i - 1) % 2][j - A[i - 1]] or f[(i - 1) % 2][j]
                else:
                    f[i % 2][j] = f[(i - 1) % 2][j]
        for j in xrange(m, -1, -1):
            if f[n % 2][j]:
                return j

```

  


