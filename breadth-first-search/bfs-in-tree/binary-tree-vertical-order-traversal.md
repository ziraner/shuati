Binary Tree Vertical Order Traversal 解题报告

Given a binary tree, return thevertical ordertraversal of its nodes' values. \(ie, from top to bottom, column by column\).

If two nodes are in the same row and column, the order should be from **left to right**.

Given binary tree`{3,9,8,4,0,1,7}`

```
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
```

Return its vertical order traversal as:`[[4],[9],[3,0,1],[8],[7]]`

Idea:

树中分层BFS的变形

将node和col作为二维tuple存进q中，将col作为key存进hashmap中，这样可以保证hashmap中col对应的array数据满足从上到下，从左到右的顺序。最后对hashmap的key排序逐个输出即为最后所求

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def verticalOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root:
            return []
        q, hm = [(root, 0)], {}
        while q:
            node, col = q.pop(0)
            if col not in hm:
                hm[col] = [node.val]
            else:
                hm[col].append(node.val)
            if node.left:
                q.append((node.left, col - 1))
            if node.right:
                q.append((node.right, col + 1))
        ans = []
        for key in sorted(hm.keys()):
            ans.append(hm[key][:])
        return ans
```



