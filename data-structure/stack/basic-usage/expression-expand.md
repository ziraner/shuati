Expression Expand 解题报告

Given an expression`s`includes numbers, letters and brackets. Number represents the number of repetitions inside the brackets\(can be a string or another expression\)．Please expand expression to be a string.

**Example**

s =`abc3[a]`return`abcaaa`  
s =`3[abc]`return`abcabcabc`  
s =`4[ac]dy`, return`acacacacdy`  
s =`3[2[ad]3[pf]]xyz`, return`adadpfpfpfadadpfpfpfadadpfpfpfxyz`

Idea：

根据遇到的情况分析

```
class Solution:
    """
    @param: s: an expression includes numbers, letters and brackets
    @return: a string
    """
    def expressionExpand(self, s):
        # write your code here
        stack = []
        num = 0
        for c in s:
            if c.isdigit():
                num = num * 10 + ord(c) - ord('0')
            elif c == '[':
                stack.append(num)
                num = 0
            elif c == ']':
                str = []
                while stack:
                    tmp = stack.pop()
                    if type(tmp) == int:
                        stack.append(''.join(str[::-1] * tmp))
                        break
                    str.append(tmp)
            else:
                stack.append(c)
        return ''.join(stack)
```



