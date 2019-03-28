Wildcard Matching 解题报告

Implement wildcard pattern matching with support for`'?'`and`'*'`.

```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the 
entire
 input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
```

Idea:

这个题跟regular expression match很类似但是也不同，因为这个题目中\*的matching跟preceding没有关系，它本身可以match一切

如果遇到了\* , 可以什么都不match: f\[i\]\[j - 1\]，可以match一个字符: f\[i - 1\]\[j - 1\]，两个字符f\[i - 2\]\[j - 1\]...

f\[i\]\[j\] = f\[i\]\[j - 1\] \|\| f\[i - 1\]\[j - 1\] \|\| f\[i - 2\]\[j - 1\] \|\| f\[i - 3\]\[j - 1\] ... \|\| f\[0\]\[j - 1\]  
f\[i - 1\]\[j\] = f\[i - 1\]\[j - 1\] \|\| f\[i - 2\]\[j - 1\] \|\| f\[i - 3\]\[j - 1\] ... \|\| f\[0\]\[j - 1\]

f\[i\]\[j\] = f\[i\]\[j - 1\] \|\| f\[i - 1\]\[j\]

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
        for j in xrange(1, n + 1):
            if p[j - 1] == '*':
                f[0][j] = f[0][j - 1]
        for i in xrange(1, m + 1):
            for j in xrange(1, n + 1):
                if p[j - 1] == '*':
                    f[i][j] = f[i][j - 1] or f[i - 1][j]
                else:
                    if p[j - 1] == '?' or p[j - 1] == s[i - 1]:
                        f[i][j] = f[i - 1][j - 1]
        return f[m][n]
```



