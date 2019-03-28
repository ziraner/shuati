Interleaving String解题报告

Given three strings:_s1_,_s2_,_s3_, determine whether_s3\_is formed by the interleaving of\_s1\_and\_s2_.

**Example**

For s1 =`"aabcc"`, s2 =`"dbbca"`

* When s3 =`"aadbbcbcac"`, return`true`.
* When s3 =`"aadbbbaccc"`, return`false`.

```
class Solution:
    """
    @param: s1: A string
    @param: s2: A string
    @param: s3: A string
    @return: Determine whether s3 is formed by interleaving of s1 and s2
    """
    def isInterleave(self, s1, s2, s3):
        # write your code here
        n1, n2, n3 = len(s1), len(s2), len(s3)
        if n1 + n2 != n3:
            return False
        dp = [[False for _ in range(n2 + 1)] for _ in range(n1 + 1)]
        dp[0][0] = True
        for i in range(1, n1 + 1):
            dp[i][0] = s1[i - 1] == s3[i - 1] and dp[i - 1][0]
        for j in range(1, n2 + 1):
            dp[0][j] = s2[j - 1] == s3[j - 1] and dp[0][j - 1]
        for i in range(1, n1 + 1):
            for j in range(1, n2 + 1):
                if s1[i - 1] == s3[i + j - 1] and dp[i - 1][j] or s2[j -1] == \
                        s3[i + j - 1] and dp[i][j - 1]:
                    dp[i][j] = True
        return dp[n1][n2]
```



