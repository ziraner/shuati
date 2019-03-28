Backpack II 解题报告

Given_n\_items with size Aiand value Vi, and a backpack with size\_m_. What's the maximum value can you put into the backpack?

**Example**

Given 4 items with size`[2, 3, 5, 7]`and value`[1, 5, 2, 4]`, and a backpack with size`10`. The maximum value is`9`.

带价值的背包问题

f\[i\]\[j\] 表示前i个物品当中选一些物品组成容量为j的最大价值

f\[i\]\[j\] = max\(f\[i-1\]\[j\], f\[i-1\]\[j-A\[i-1\]\] + V\[i-1\]\);

f\[0\]\[0\]=0

f\[n\]\[s\]

```
class Solution:
    """
    @param: m: An integer m denotes the size of a backpack
    @param: A: Given n items with size A[i]
    @param: V: Given n items with value V[i]
    @return: The maximum value
    """
    def backPackII(self, m, A, V):
        # write your code here
        if not A or not V:
            return 0
        n = len(A)
        f = [[0 for _ in xrange(m + 1)] for _ in xrange(2)]
        for i in xrange(1, n + 1):
            for j in xrange(1, m + 1):
                f[i % 2][j] = f[(i - 1) % 2][j]
                if j >= A[i - 1]:
                    val = f[(i - 1) % 2][j - A[i - 1]] + V[i - 1]
                    f[i % 2][j] = max(val, f[(i - 1) % 2][j])
        return f[n % 2][m]
```



