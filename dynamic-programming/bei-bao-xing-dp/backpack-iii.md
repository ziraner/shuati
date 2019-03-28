Backpack III 解题报告

Given_n\_kind of items with size Aiand value Vi\(_`each item has an infinite number available`_\) and a backpack with size\_m_. What's the maximum value can you put into the backpack?

**Example**

Given 4 items with size`[2, 3, 5, 7]`and value`[1, 5, 2, 4]`, and a backpack with size`10`. The maximum value is`15`.

带价值的无限背包问题

可以用三层循环解，但是不是最优解，利用完全背包问题时间复杂度的改善解法：

f\[i\]\[j\] = max\(f\[i\]\[j - A\[i - 1\]\] + V\[i - 1\], f\[i\]\[j\]\)

注意这里f\[i\]\[j - A\[i - 1\]\)这个是和BackPack II最大的区别，backpack II是

f\[i\]\[j\] = max\(f\[i - 1\]\[j - A\[i - 1\]\] + V\[i - 1\], f\[i\]\[j\]\)

时间复杂度是O\(n \* S\)

```
class Solution:
    """
    @param: A: an integer array
    @param: V: an integer array
    @param: m: An integer
    @return: an array
    """
    def backPackIII(self, A, V, m):
        # write your code here
        if not A or not V:
            return 0
        n = len(A)
        f = [[0 for _ in xrange(m + 1)] for _ in xrange(2)]
        for i in xrange(1, n + 1):
            for j in xrange(1, m + 1):
                # don't choose A[i-1]
                f[i % 2][j] = f[(i - 1) % 2][j]
                # no need to loop k since it is already covered by increasing j
                if j >= A[i - 1]:
                    # f[i][j - A[i - 1]] is already calculated max of all k before
                    # this is the only difference from BackPack II
                    val = f[i % 2][j - A[i - 1]] + V[i - 1]
                    f[i % 2][j] = max(val, f[i % 2][j])
        return f[n % 2][m]
```



