Excel Sheet Column Number解题报告

Related to question[Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
```

idea:

是上一个题的逆版

注意ans 要加1

```
class Solution(object):
    def titleToNumber(self, s):
        """
        :type s: str
        :rtype: int
        """
        MAP = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
        ans = 0
        for c in s:
            idx = MAP.find(c)
            ans = ans * 26 + idx + 1
        return ans
```



