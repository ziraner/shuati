Sum of Left Leaves 解题报告

Find the sum of all left leaves in a given binary tree.

**Example:**

```
    3
   / \
  9  20
    /  \
   15   7
There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

Idea:

divide and conquer, helper 函数传递两个变量，是否为左子树和当前root

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sumOfLeftLeaves(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        return self.helper(root, False)
    def helper(self, root, isLeft):
        if not root:
            return 0
        if not root.left and not root.right:
            if isLeft:
                return root.val
            return 0
        return self.helper(root.left, True) + self.helper(root.right, False)
```



  


