Subtree of Another Tree 解题报告

Given two non-empty binary trees  **s **and **t**, check whether tree **t **has exactly the same structure and node values with a subtree of **s**. A subtree of **s **is a tree consists of a node in  **s **and all of this node's descendants. The tree **s **could also be considered as a subtree of itself.

**Example 1:**  
Given tree s:

```
     3
    / \
   4   5
  / \
 1   2
```

Given tree t:

```
   4 
  / \
 1   2
```

Return **true**, because t has the same structure and node values with a subtree of s.

Idea:

为了方便写，把isSame和isSubtree写成两个递归函数，且不容易出错儿

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isSubtree(self, s, t):
        """
        :type s: TreeNode
        :type t: TreeNode
        :rtype: bool
        """
        if not s and not t:
            return True
        if not s or not t:
            return False
        if self.isSame(s, t):
            return True
        return self.isSubtree(s.left, t) or self.isSubtree(s.right, t)
    def isSame(self, s, t):
        if not s and not t:
            return True
        if not s or not t:
            return False
        if s.val != t.val:
            return False
        return self.isSame(s.left, t.left) and self.isSame(s.right, t.right)
```



