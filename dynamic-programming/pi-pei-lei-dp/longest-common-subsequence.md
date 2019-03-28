Longest Common Subsequence 解题报告Longest Common Subsequence解题报告

Given two strings, find the longest common subsequence \(_LCS_\).

Your code should return the length of_LCS_.

**Example**

For`"ABCD"`and`"EDCA"`, the\_LCS\_is`"A"`\(or`"D"`,`"C"`\), return`1`.

For`"ABCD"`and`"EACB"`, the\_LCS\_is`"AC"`, return`2`.

匹配类DP

state: f\[i\]\[j\]表示前i个字符配上前j个字符的LCS的长度

function: f\[i\]\[j\] = MAX\(f\[i-1\]\[j\], f\[i\]\[j-1\], f\[i-1\]\[j-1\] + 1\) // A\[i - 1\] == B\[j - 1\]

                         = MAX\(f\[i-1\]\[j\], f\[i\]\[j-1\]\) // A\[i - 1\] != B\[j - 1\]

intialize: f\[i\]\[0\] = 0 f\[0\]\[j\] = 0

answer: f\[n\]\[m\]

```
class Solution:
    """
    @param: A: A string
    @param: B: A string
    @return: The length of longest common subsequence of A and B
    """
    def longestCommonSubsequence(self, A, B):
        # write your code here
        m, n = len(A), len(B)
        f = [[0 for _ in range(n + 1)] for _ in range(m + 1)]
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if A[i - 1] == B[j - 1]:
                    f[i][j] = f[i - 1][j - 1] + 1
                else:
                    f[i][j] = max(f[i][j - 1], f[i - 1][j])
        return f[m][n]
```



