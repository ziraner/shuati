Shortest Palindrome 解题报告

Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

For example:

Given`"aacecaaa"`, return`"aaacecaaa"`.

Given`"abcd"`, return`"dcbabcd"`.

暴力解法：O\(n^2\)

从尾开始，每次去掉一个验证前面是否是palindrome是的话讲当前的尾部翻转放前面既可

```
class Solution(object):
    def shortestPalindrome(self, s):
        for i in xrange(len(s), -1, -1):
            if self.isP(s[:i]):
                return s[i:][::-1] + s
        return ''
    def isP(self, s):
        i, j = 0, len(s) - 1
        while i < j:
            if s[i] != s[j]:
                return False
            i += 1
            j -= 1
        return True
```

KMP做法：O\(n\)

这个问题本质上是找从头开始最长的palindrome长度（或者是什么）， 想到了用KMP中next数组的方法，将原字符串转化成：  
s + '$' + s\[::-1\]的格式，然后找p\[-1\]的值即为可以去的最长的s\[::-1\]中的地方继续匹配。所以答案就是s\[::-1\]\[:len\(s\) - 1- p\[-1\]\] + s

```
class Solution(object):
    def shortestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        new_s = s[::-1] + '$' + s
        print new_s
        n = len(new_s)
        p = [0 for _ in xrange(n)]
        p[0] = -1
        k = -1
        for j in xrange(1, n):
            while k != -1 and new_s[k + 1] != new_s[j]:
                k = p[k]
            if new_s[k + 1] == new_s[j]:
                k += 1
            p[j] = k
        print p
        length = max(p)
        return s[length + 1:][::-1] + s
```

  


