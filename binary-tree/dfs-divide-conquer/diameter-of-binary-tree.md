Diameter of Binary Tree 解题报告

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the**longest**path between any two nodes in a tree. This path may or may not pass through the root.

**Example:**  
Given a binary tree

```
          1
         / \
        2   3
       / \     
      4   5    
```

Return**3**, which is the length of the path \[4,2,1,3\] or \[5,2,1,3\].

Idea:

分治法。

当前root的diameter = max\( leftdiameter,  rightdiameter, maxleftdepth + maxrightdepth\)

维护两个返回变量既可

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        _, diameter = self.helper(root)
        return diameter
    def helper(self, root):
        if not root:
            return 0, 0
        l_depth, l_diameter = self.helper(root.left)
        r_depth, r_diameter = self.helper(root.right)
        return (max(l_depth, r_depth) + 1, max(l_diameter, r_diameter, l_depth + r_depth)) 
```



