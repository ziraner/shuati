k Sum解题报告

Given_n_distinct positive integers, integer_k_\(_k_&lt;=_n_\) and a number_target_.

Find_k_numbers where sum is target. Calculate how many solutions there are?

**Example**

Given`[1,2,3,4]`, k =`2`, target =`5`.

There are`2`solutions:`[1,4]`and`[2,3]`.

Return`2`.

三维的背包问题

f\[i\]\[j\]\[t\]前i个数取j个数出来和为t的solution的数目 

f\[i\]\[j\]\[t\] = f\[i - 1\]\[j - 1\]\[t - a\[i-1\]\] + f\[i - 1\]\[j\]\[t\]

f\[i\]\[0\]\[0\] = 1

f\[n\]\[k\]\[target\]

```
class Solution:
    """
    @param: A: An integer array
    @param: k: A positive integer (k <= length(A))
    @param: target: An integer
    @return: An integer
    """
    def kSum(self, A, k, target):
        # write your code here
        # f[i][j][s]: qian i ge pick j ge shu sum wei s
        n = len(A)
        f = [[[0 for _ in xrange(target + 1)] for _ in xrange(k + 1) ] for _ in xrange(n + 1)]
        for i in xrange(n + 1):
            f[i][0][0] = 1
        for i in xrange(1, n + 1):
            for j in xrange(1, i + 1):
                if j > k:
                    break
                for s in xrange(1, target + 1):
                    if s >= A[i - 1]:
                        f[i][j][s] = f[i - 1][j][s] + f[i - 1][j - 1][s - A[i - 1]]
                    else:
                        f[i][j][s] = f[i - 1][j][s]
        return f[n][k][target]
```



