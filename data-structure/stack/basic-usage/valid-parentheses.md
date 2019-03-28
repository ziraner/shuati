Valid Parentheses 解题报告

Given a string containing just the characters`'('`,`')'`,`'{'`,`'}'`,`'['`and`']'`, determine if the input string is valid.

The brackets must close in the correct order,`"()"`and`"()[]{}"`are all valid but`"(]"`and`"([)]"`are not.

Idea:

用stack

注意在pop的时候先确认stack是否不为空；最后返回的时候要确认stack是否为空

```
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        for c in s:
            if c in '[{(':
                stack.append(c)
            else:
                if not stack or stack.pop() + c not in ['()', '[]', '{}']:
                    return False
        return not stack
```





