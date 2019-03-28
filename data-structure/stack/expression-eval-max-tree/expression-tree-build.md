Expression Tree Build解题报告

The structure of Expression Tree is a binary tree to evaluate certain expressions.  
All leaves of the Expression Tree have an number string value. All non-leaves of the Expression Tree have an operator string value.

Now, given an expression array, build the expression tree of this expression, return the root of this expression tree.

**Example**

For the expression`(2*6-(23+7)/(1+2))`\(which can be represented by \["2" "\*" "6" "-" "\(" "23" "+" "7" "\)" "/" "\(" "1" "+" "2" "\)"\]\).  
The expression tree will be like

```
                 [ - ]
             /          \
        [ * ]              [ / ]
      /     \           /         \
    [ 2 ]  [ 6 ]      [ + ]        [ + ]
                     /    \       /      \
                   [ 23 ][ 7 ] [ 1 ]   [ 2 ] .
```

After building the tree, you just need to return root node`[-]`.

Idea：

这个题很牛逼，是带括号expression evaluation的关键一环。

build出来的这个tree，中序遍历是expression本身，后序遍历是reversed polish notation，前序遍历是polish notation。

而计算机可以很轻松的用polish notation和reversed polish notation evaluate expression。

对于build tree expression这个题目来说，需要calculate每个item的权重，然后构建一个最小数，权重最小的放在root。  
num: val = maxint  
\(\)里面的每一层括号 + 10  
+/- +1  
\* / +2  
对除了括号之外的每个item算一个val然后按照Max Tree类似的方法，建一个单调增的stack，从而去建立一个Min Tree

因为题目的ExpressionNode只有symbol没有val所以还要自己建一个TreeNode，包含enode和val

```
"""
Definition of ExpressionTreeNode:
class ExpressionTreeNode:
    def __init__(self, symbol):
        self.symbol = symbol
        self.left, self.right = None, None
"""
from sys import maxint

class Solution:
    """
    @param: expression: A string array
    @return: The root of expression tree
    """
    def build(self, expression):
        # write your code here
        # evaluate the value of each operator in the tree:
        # within (): val += 10; +/-: val += 1; * /: val += 2; int: val = MAX
        # build a min tree based on values
        if not expression:
            return None
        base, val = 0, 0
        stack = []
        for symbol in expression:
            if symbol == '(':
                base += 10
                continue
            if symbol == ')':
                base -= 10
                continue
            val = self.getVal(symbol, base)
            node = NewNode(symbol, val)
            while stack and stack[-1].val >= val:
                node.enode.left = stack.pop().enode
            if stack:
                stack[-1].enode.right = node.enode
            stack.append(node)
        if stack:
            return stack[0].enode
        return None
    def getVal(self, symbol, base):
        if symbol == '+' or symbol == '-':
            if symbol == '999':
                print "1"
            return 1 + base
        if symbol == '*' or symbol == '/':
            if symbol == '999':
                print '2'
            return 2 + base
        if symbol == '999':
            print "hello"
        return maxint
class NewNode:
    def __init__(self, symbol, val):
        self.enode = ExpressionTreeNode(symbol)
        self.val = val
```



