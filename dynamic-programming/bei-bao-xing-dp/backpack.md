Bacpack 解题报告

Given n items with size Ai, an integer m denotes the size of a backpack. How full you can fill this backpack?

**Notice**

You can not divide any item into small pieces.

**Example**

If we have`4`items with size`[2, 3, 5, 7]`, the backpack size is 11, we can select`[2, 3, 5]`, so that the max size we can fill this backpack is`10`. If the backpack size is`12`. we can select`[2, 3, 7]`so that we can fulfill the backpack.

You function should return the max size we can fill in the given backpack.

**Idea**

背包类DP

1. 定义：f[i][S] “前i”个物品，取出一些能否组成和为S；即i多定义了一位

2. 转移方程：f[i][S] = f[i-1][S - a[i-1]] or f[i-1][S]。即如果前i-1个物品已经组成S，那么前i个物品一定可以组成S；如果前i-1个物品可以组成S-a[i -1]那么前i个物品一定可以组成S。 a[i-1] 是第i个物品下标是i-1

3. 初始化：f[i][0] = true，即前i个物体一定可以组成重量0; f[0][1..target] = false，即前0个物体一定不能组成任何非0重量。

4. 答案：倒叙检查f[n][j]，即前n个物体组成的每个重量从大到小排列，第一个出现的就是最大重量。

时间复杂度O(n*S)，空间复杂度O(S)因为可以用滚动数组优化。

```python
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
