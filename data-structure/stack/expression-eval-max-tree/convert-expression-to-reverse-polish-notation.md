Convert Expression to Reverse Polish Notation解题报告

Given an expression string array, return the Reverse Polish notation of this expression. \(remove the parentheses\)

Reverse Polish Notation是expression tree的后序遍历

evaluate reverse polsih notation的方法是从左向右扫，遇到数字进栈，遇到操作符从栈中pop出两个，操作完了把结果入栈。需要注意的是如果是a - b的话先pop出来的是b后pop出来的是a，这点跟polish notation不一样

```
from sys import maxint
class Solution:
    """
    @param: expression: A string array
    @return: The Reverse Polish notation of this expression
    """
    def convertToRPN(self, expression):
        # write your code here
        if not expression:
            return None
        root = self.convertToTree(expression)
        ans = []
        self.dfs(root, ans)
        return ans 
    def dfs(self, root, ans):
        if not root:
            return
        self.dfs(root.left, ans)
        self.dfs(root.right, ans)
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
        if symbol == '/' or symbol == '*':
            return base + 2
        if symbol == '+' or symbol == '-':
            return base + 1
        return maxint
class TreeNode1:
    def __init__(self, val, symbol):
        self.val = val
        self.symbol = symbol
        self.right = None
        self.left = None
```



