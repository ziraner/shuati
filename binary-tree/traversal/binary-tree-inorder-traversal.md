Binary Tree Inorder Traversal 解题报告

Given a binary tree, return the inorder traversal of its nodes' values.

Idea:

非递归怎么写？背

```
class Solution:
    """
    @param root: The root of binary tree.
    @return: Inorder in ArrayList which contains node values.
    """
    def inorderTraversal(self, root):
        # write your code here
        if not root:
            return []
        stack, ans = [], []
        cur = root
        while cur or stack:
            while cur:
                stack.append(cur)
                cur = cur.left
            cur = stack.pop()
            ans.append(cur.val)
            cur = cur.right
        return ans
```



