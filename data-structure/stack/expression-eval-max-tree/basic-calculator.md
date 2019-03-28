Basic Calculator 解题报告

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open`(`and closing parentheses`)`, the plus`+`or minus sign`-`,**non-negative**integers and empty spaces.

You may assume that the given expression is always valid.

Some examples:

```
"1 + 1" = 2
" 2-1 + 2 " = 3
"(1+(4+5+2)-3)+(6+8)" = 23

```

**Note:Do not**use the`eval`built-in library function.

思路：

这个题也是一道计算表达式值的题目，但是不一样的点是表达式是string空格可能存在可能不存在；且只有+-没有\*/

想法是递归遇到括号递归到下一层计算，下一层计算完了值返回当前层

因为是递归来做expression evaluate的过程所以需要有一个全局变量统计现在走到哪个position了。

在递归函数中，因为是落后一个运算次序的，所以需要有一个状态来表明之前那步是减号还是加号。

递归函数中，遇到左括号，pos需要+1否则无限爆栈；而遇到右括号就不需要pos + 1因为遇到右括号返回到之前的函数里面了，之前函数里面的位置是左括号的位置，在执行完左括号逻辑之后，pos会在循环中自动+ 1

如果遇到左括号的话，可以将expression想象成一个num，因为不能想象成运算符，就只能想象成num

ans只在运算符逻辑和最后返回逻辑之前进行运算。

```
class Solution(object):
    def calculate(self, s):
        """
        :type s: str
        :rtype: int
        """
        new_s = "(" + s + ")"
        self.pos = 1
        return self.dfs(new_s)
    def dfs(self, s):
        ans, num, status = 0, 0, 'plus'
        smap = {'plus': 1, 'minus': -1}
        while self.pos < len(s):
            if s[self.pos].isdigit():
                num = 10 * num + ord(s[self.pos]) - ord('0')
            elif s[self.pos] == '+':
                ans += smap[status] * num
                num = 0
                status = 'plus'
            elif s[self.pos] == '-':
                ans += smap[status] * num
                num = 0
                status = 'minus'
            elif s[self.pos] == '(':
                self.pos += 1
                num = self.dfs(s)
            elif s[self.pos] == ')':
                ans += smap[status] * num
                return ans
            self.pos += 1
        return ans
```

  


