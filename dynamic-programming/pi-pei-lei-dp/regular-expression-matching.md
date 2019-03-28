Regular Expression Matching解题报告

Implement regular expression matching with support for`'.'`and`'*'`.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the 
entire
 input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

idea:

匹配类DP f\[i\]\[j\]表示s的前i个字符匹配上p的前j个字符是否match。具体方程见代码。这个题有个点需要注意的是裸“.\*”可以匹配一切字符，虽然看起来很不合理，但是根据题目的rule这是必然的可以强行记住

```
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        m, n = len(s), len(p)
        f = [[False for _ in xrange(n + 1)] for _ in xrange(m + 1)]
        f[0][0] = True
        for j in xrange(2, n + 1):
            if p[j - 1] == '*':
                f[0][j] = f[0][j - 2]
        for i in xrange(1, m + 1):
            for j in xrange(1, n + 1):
                if p[j - 1] == '*':
                    if p[j - 2] == '.' or p[j - 2] == s[i - 1]:
                        f[i][j] = f[i][j - 2] or f[i - 1][j]
                    else:
                        f[i][j] = f[i][j - 2]
                else:
                    if p[j - 1] == '.' or p[j - 1] == s[i - 1]:
                        f[i][j] = f[i - 1][j - 1]
        return f[m][n]
```



