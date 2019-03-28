Expression Evaluation 解题报告

Given an expression string array, return the final result of this expression

The expression contains only`integer`,`+`,`-`,`*`,`/`,`(`,`)`.

**Example**

For the expression`2*6-(23+7)/(1+2)`,  
input is

```
[
  "2", "*", "6", "-", "(",
  "23", "+", "7", ")", "/",
  "(", "1", "+", "2", ")"
],

```

return`2`

Idea

我们有两种思路，先将expression转换成polish notation然后再求值，或者是将expression转换成reversed polish notation然后再求值。

Polish Notation

```
from sys import maxint
class Solution:
    """
    @param: expression: a list of strings
    @return: an integer
    """
    def evaluateExpression(self, expression):
        # write your code here
        pn = self.convertToPN(expression)
        operators = ['+', '-', '*', '/']
        stack = []
        for i in xrange(len(pn) - 1, - 1, -1):
            if pn[i] not in operators:
                stack.append(int(pn[i]))
            else:
                num1 = stack.pop()
                num2 = stack.pop()
                num = 0
                if pn[i] == '+': num = num1 + num2
                elif pn[i] == '-': num = num1 - num2
                elif pn[i] == '*': num = num1 * num2
                else: num = int(num1 * 1.0 / num2)
                stack.append(num)
        if not stack:
            return 0
        return stack[0]
    def convertToPN(self, expression):
        root = self.convertToTree(expression)
        ans = []
        self.dfs(ans, root)
        return ans
    def dfs(self, ans, root):
        if not root:
            return
        ans.append(root.symbol)
        self.dfs(ans, root.left)
        self.dfs(ans, root.right)
    def convertToTree(self, expression):
        base, val = 0, 0
        stack = []
        for symbol in expression:
            if symbol == '(':
                base += 10
                continue
            if symbol == ')':
                base -= 10
                continue
            val = self.getVal(base, symbol)
            node = TreeNode1(val, symbol)
            while stack and stack[-1].val >= node.val:
                node.left = stack.pop()
            if stack:
                stack[-1].right = node
            stack.append(node)
        if not stack:
            return None
        return stack[0]
    def getVal(self, base, symbol):
        if symbol == '+' or symbol == '-':
            return base + 1
        if symbol == '*' or symbol == '/':
            return base + 2
        return maxint
class TreeNode1:
    def __init__(self, val, symbol):
        self.val = val
        self.symbol = symbol
        self.right = None
        self.left = None
```

Reversed Polish Notation

```
from sys import maxint
class Solution:
    """
    @param: expression: a list of strings
    @return: an integer
    """
    def evaluateExpression(self, expression):
        # write your code here
        # Reversed Polish Notation
        return self.evaluateRPN(expression)
    def evaluateRPN(self, expression):
        rpn = self.convertToRPN(expression)
        stack = []
        for symbol in rpn:
            num = 0
            if symbol in '+-*/':
                num2 = stack.pop()
                num1 = stack.pop()
                if symbol == '+':
                    num = num1 + num2
                elif symbol == '-':
                    num = num1 - num2
                elif symbol == '*':
                    num = num1 * num2
                else:
                    num = int(num1 * 1.0 / num2)
            else:
                num = int(symbol)
            stack.append(num)
        if stack:
            return stack.pop()
        return 0
    def convertToRPN(self, expression):
        root = self.convertToTree(expression)
        ans = []
        self.traverse(ans, root)
        return ans
    def traverse(self, ans, root):
        if not root:
            return
        self.traverse(ans, root.left)
        self.traverse(ans, root.right)
        ans.append(root.symbol)
    def convertToTree(self, expression):
        base, val = 0, 0
        stack = []
        for symbol in expression:
            if symbol == '(':
                base += 10
                continue
            if symbol == ')':
                base -= 10
                continue
            val = self.getVal(base, symbol)
            node = TreeNode1(val, symbol)
            while stack and stack[-1].val >= node.val:
                node.left = stack.pop()
            if stack:
                stack[-1].right = node
            stack.append(node)
        if not stack:
            return None
        return stack[0]
    def getVal(self, base, symbol):
        if symbol == '+' or symbol == '-':
            return base + 1
        if symbol == '*' or symbol == '/':
            return base + 2
        return maxint
class TreeNode1:
    def __init__(self, val, symbol):
        self.val = val
        self.symbol = symbol
        self.right = None
        self.left = None
```



