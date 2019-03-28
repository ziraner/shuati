Distinct Subsequences 解题报告

Given a string**S**and a string**T**, count the number of distinct subsequences of**T**in**S**.

A subsequence of a string is a new string which is formed from the original string by deleting some \(can be none\) of the characters without disturbing the relative positions of the remaining characters. \(ie,`"ACE"`is a subsequence of`"ABCDE"`while`"AEC"`is not\).

**Example**

Given S =`"rabbbit"`, T =`"rabbit"`, return`3`.

匹配类DP

state: f\[i\]\[j\] 表示 S的前i个字符中选取T的前j个字符，有多少种方案

function: f\[i\]\[j\] = f\[i - 1\]\[j\] + f\[i - 1\]\[j - 1\] // S\[i-1\] == T\[j-1\]

                         = f\[i - 1\]\[j\] // S\[i-1\] != T\[j-1\]

initialize: f\[i\]\[0\] = 1, f\[0\]\[j\] = 0 \(j &gt; 0\)

answer: f\[n\]\[m\] \(n = sizeof\(S\), m = sizeof\(T\)\)  


```
class Solution:
    """
    @param: : A string
    @param: : A string
    @return: Count the number of distinct subsequences
    """

    def numDistinct(self, S, T):
        # write your code here
        # state: f[i][j] S total number of distsub for S: 0 ~ i - 1 T: 0 ~ j -1
        m, n = len(S), len(T)
        f = [[0 for _ in xrange(n + 1)] for _ in xrange(m + 1)]
        for i in xrange(m + 1):
            f[i][0] = 1
        for i in xrange(1, m + 1):
            for j in xrange(1, n + 1):
                if S[i - 1] != T[j - 1]:
                    f[i][j] = f[i - 1][j]
                else:
                    f[i][j] = f[i - 1][j] + f[i - 1][j - 1]
        return f[m][n]
```



