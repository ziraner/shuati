Binary Tree Preorder Traversal 解题报告

Given a binary tree, return the preorder traversal of its nodes' values.

Idea:

非递归怎么写？跟树上的BFS相反，用stack，每次将栈顶元素弹出加入solution，然后依次将元素的右子树和左子树压栈。

```
class Solution:
    """
    @param root: The root of binary tree.
    @return: Preorder in ArrayList which contains node values.
    """
    def preorderTraversal(self, root):
        # write your code here
        """ recursion
        if root:
           return [root.val] + self.preorderTraversal(root.left) \
                + self.preorderTraversal(root.right)
        return []
        """
        # non-recursion
        if not root:
            return []
        stack, ans = [root], []
        while stack:
            tmp = stack.pop()
            ans.append(tmp.val)
            if tmp.right:
                stack.append(tmp.right)
            if tmp.left:
                stack.append(tmp.left)
        return ans
```



