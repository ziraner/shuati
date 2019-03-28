Valid Number 解题报告

Validate if a given string is numeric.

Some examples:  
`"0"`=&gt;`true`  
`" 0.1 "`=&gt;`true`  
`"abc"`=&gt;`false`  
`"1 a"`=&gt;`false`  
`"2e10"`=&gt;`true`  


**Note:**It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

Idea:

三个flag变量，num，exp，dot表示是否是这些东西  
e/E：只能出现在not exp and num的情况，出现之后exp = True，num = False  
+/-：只可能出现在字符串的开始或者前一位是E的情况  
.：只可能出现在not exp and not dot的地方  
0123456789：num = True  
然后逐一讨论，这些东西如果出现可以出现的地方。对前三种分别建一个flag来表示它出现过没有

```
class Solution(object):
    def isNumber(self, s):
        """
        :type s: str
        :rtype: bool
        """
        s = s.strip()
        i, n = 0, len(s)
        num, exp, dot = False, False, False
        while i < n:
            if s[i] in "+-":
                if i != 0 and s[i - 1] not in 'eE':
                    return False
            elif s[i] in "eE":
                if not num or exp:
                    return False
                exp = True
                num = False
            elif s[i] == '.':
                if dot or exp:
                    return False
                dot = True
            elif s[i].isdigit():
                num = True
            else:
                return False
            i += 1
        return num

```



