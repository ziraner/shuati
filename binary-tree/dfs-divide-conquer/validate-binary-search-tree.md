Validate Binary Search Tree 解题报告

Given a binary tree, determine if it is a valid binary search tree \(BST\).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys l**ess than **the node's key.
* The right subtree of a node contains only nodes with keys **greater than **the node's key.
* Both the left and right subtrees must also be binary search trees.

**Example 1:**

```
    2
   / \
  1   3
```

Binary tree`[2,1,3]`, return true.

Idea:

三个返回值：isBst, maxVal, minVal

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        isBst, _, _ = self.helper(root)
        return isBst
    def helper(self, root):
        from sys import maxint
        if not root:
            return True, -maxint, maxint
        l_isBst, l_maxVal, l_minVal = self.helper(root.left)
        r_isBst, r_maxVal, r_minVal = self.helper(root.right)
        if not l_isBst or not r_isBst:
            return False, 0, 0
        if root.left and l_maxVal >= root.val:
            return False, 0, 0
        if root.right and r_minVal <= root.val:
            return False, 0, 0
        return True, max(root.val, r_maxVal), min(root.val, l_minVal)
```



