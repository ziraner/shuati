Excel Sheet Column Title解题报告

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

```
1 -> A
2 -> B
3 -> C
...
26 -> Z
27 -> AA
28 -> AB 
```

Idea:

跟罗马的题目比较像

可以看成是一道进制转换类的题目

```
class Solution(object):
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        MAP = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
        ans = ''
        while n != 0:
            idx = (n - 1) % 26
            ans = MAP[idx] + ans
            n = (n - 1) / 26
        return ans
```



