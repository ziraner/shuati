Convert Expression to Polish Notation解题报告

Given an expression string array, return the Polish notation of this expression. \(remove the parentheses\)

Polish Notation是expression tree是前序遍历

evaluate polish notation的方法是从右向左扫描，遇到num进栈，遇到操作符弹出两个num计算然后结果继续入栈。需要注意的是如果是a-b的话先pop出来的是a后pop出来的是b，跟reversed polish notation不同

```
from sys import maxint
class Solution:
    """
    @param: expression: A string array
    @return: The Polish notation of this expression
    """
    def convertToPN(self, expression):
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
        ans.append(root.symbol)
        self.dfs(root.left, ans)
        self.dfs(root.right, ans)
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
        val = 0
        if symbol == '*' or symbol == '/':
            val = base + 2
        elif symbol == '+' or symbol == '-':
            val = base + 1
        else:
            val = maxint
        return val
class TreeNode1:
    def __init__(self, val, symbol):
        self.val = val
        self.symbol = symbol
        self.right = None
        self.left = None
```



