Average of Levels in Binary Tree 解题报告

Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.

**Example 1:**

```
Input:

    3
   / \
  9  20
    /  \
   15   7

Output:[3, 14.5, 11]
Explanation:
The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
```

Idea:

树的分层BFS

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def averageOfLevels(self, root):
        """
        :type root: TreeNode
        :rtype: List[float]
        """
        if not root:
            return []
        q, ans = [root], []
        while q:
            size = len(q)
            level = []
            for i in xrange(size):
                tmp = q.pop(0)
                level.append(tmp.val)
                if tmp.left:
                    q.append(tmp.left)
                if tmp.right:
                    q.append(tmp.right)
            ans.append(sum(level) * 1.0 / len(level))
        return ans
```



