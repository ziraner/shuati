Basic Calculator II解题报告

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only**non-negative**integers,`+`,`-`,`*`,`/`operators and empty spaces. The integer division should truncate toward zero.

You may assume that the given expression is always valid.

Some examples:  


```
"3+2*2" = 7
" 3/2 " = 1
" 3+5 / 2 " = 5
```

**Note:Do not**use the`eval`built-in library function.

Idea

这个题目也是expression evaluation好处是没有括号。但是有加减乘除四则运算，以及可能会有空格，以及input是string的形式

这个题不同于basic calculatorI，如果保存之前的符号是啥，以及结合当前的符号是啥过于复杂。所以我们采取add operator那个题的形式，保存一个ans和一个lastF两个变量，而且我们定义一个getNum函数专门取数，取出来的数保存进num

和addoperator那个题不一样的点在于，多了一个除法，注意python对于负整数的除法很操蛋，需要判断lastF是负的还是正的

```
class Solution(object):
    def calculate(self, s):
        """
        :type s: str
        :rtype: int
        """
        i, ans = self.getNum(s, 0)
        lastF = ans
        while i < len(s):
            if s[i] == ' ':
                i += 1
            else:
                next_i, num = self.getNum(s, i + 1)
                if s[i] == '+':
                    ans += num
                    lastF = num
                elif s[i] == '-':
                    ans -= num
                    lastF = -num
                elif s[i] == '*':
                    ans = ans - lastF + lastF * num
                    lastF = lastF * num
                else:
                    if lastF < 0:
                        val = -lastF / num
                        ans = ans - lastF - val
                        lastF = -val
                    else:
                        val = lastF / num
                        ans = ans - lastF + val
                        lastF = val
                i = next_i
        return ans
    def getNum(self, s, pos):
        i = pos
        num = 0
        while i < len(s) and (s[i] == ' ' or s[i].isdigit()):
            if s[i].isdigit():
                num = num * 10 + ord(s[i]) - ord('0')
            i += 1
        return i, num

```



