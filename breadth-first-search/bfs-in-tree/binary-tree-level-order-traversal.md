LintCode 69. Binary Tree Level Order Traversal

**Problem**

Given a binary tree, return thelevel ordertraversal of its nodes' values. \(ie, from left to right, level by level\).

**Example**

Given binary tree`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

**Idea**

分层BFS，需要多一层循环来固定queue中的当前层的size

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root:
            return []
        q, ans = [root], []
        while q:
            level = []
            size = len(q)
            for i in xrange(size):
                node = q.pop(0)
                level.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            ans.append(level[:])
        return ans
```
