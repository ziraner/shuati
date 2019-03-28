One Edit Distance 解题报告

Given two strings S and T, determine if they are both one edit distance apart.

Idea:

edit的方式：insert, delete, replace

可以将insert和delete合并，即删除和替换两种情况讨论：

```
class Solution(object):
    def isOneEditDistance(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        m, n = len(s), len(t)
        if m < n:
            return self.isOneEditDistance(t, s)
        if m - n > 1:
            return False
        i = 0
        while i < n:
            if s[i] != t[i]:
                if m == n:
                    return s[i + 1:] == t[i + 1:]
                return s[i + 1:] == t[i:]
            i += 1
        return i == m - 1
```



