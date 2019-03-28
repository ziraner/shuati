Binary Search Tree Iterator 解题报告

Implement an iterator over a binary search tree \(BST\). Your iterator will be initialized with the root node of a BST.

Calling`next()`will return the next smallest number in the BST.

**Note:**`next()`and`hasNext()`should run in average O\(1\) time and uses O\(h\) memory, wherehis the height of the tree.

Idea:

这个题目要求avg O\(1\)时间复杂度和O\(h\)的空间复杂度，就不能够一股脑把中序遍历都找出来存在array中否则空间复杂度不OK

则想到用Binary Tree Inorder Traversal的非递归解法。其实本质是将外层的while循环拆开来，把每一步填进对应的函数中。

```
# Definition for a  binary tree node
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class BSTIterator(object):
    def __init__(self, root):
        """
        :type root: TreeNode
        """
        self.stack = []
        self.curt = root

    def hasNext(self):
        """
        :rtype: bool
        """
        while self.curt:
            self.stack.append(self.curt)
            self.curt = self.curt.left
        return len(self.stack) != 0

    def next(self):
        """
        :rtype: int
        """
        val = -1
        if self.hasNext():
            self.curt = self.stack.pop()
            val = self.curt.val
            self.curt = self.curt.right
        return val

# Your BSTIterator will be called like this:
# i, v = BSTIterator(root), []
# while i.hasNext(): v.append(i.next())
```



