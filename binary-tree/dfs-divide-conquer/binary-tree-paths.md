LintCode 480. Binary Tree Paths

**Problem**

Given a binary tree, return all root-to-leaf paths.

For example, given the following binary tree:

```
   1
 /   \
2     3
 \
  5
```

All root-to-leaf paths are:

```
["1->2->5", "1->3"]
```

Idea:

Divide & Conquer.

将从左子树得到的path加入当前节点，将整体加入当前解；将右子树得到path加入当前节点，将整体加入当前解。注意判断当前点是leaf的情况，也就是左右子树的paths都是空， 这时不加入“-&gt;”符号

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def binaryTreePaths(self, root):
        """
        :type root: TreeNode
        :rtype: List[str]
        """
        ans = []
        if not root:
            return ans
        left = self.binaryTreePaths(root.left)
        right = self.binaryTreePaths(root.right)
        for path in left:
            ans.append(str(root.val) + "->" + path)
        for path in right:
            ans.append(str(root.val) + "->" + path)
        if not left and not right:
            ans.append(str(root.val))
        return ans
```
