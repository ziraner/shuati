Inorder Successor in Binary Search Tree 解题报告

Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

Idea:

recursion: 

比较root和p如果小于等于则successor在右子树，递归在右子树中找

如果大于那么successor要么在左子树要么是本身

```
class Solution(object):
    def inorderSuccessor(self, root, p):
        """
        :type root: TreeNode
        :type p: TreeNode
        :rtype: TreeNode
        """
        # recursion
        if not root or not p:
            return None
        if root.val <= p.val:
            return self.inorderSuccessor(root.right, p)
        successor = self.inorderSuccessor(root.left, p)
        if successor:
            return successor
        return root
```

non-recursion:

先确定q的位置

while循环找q，找到退出，如果向左走则记录successor为当前的root，向右走则不需要记录

退出之后判断root.right是否存在如果不存在则返回successor，为上一个parent node

如果存在则successor为当前root右子树的最左点，循环找到它

```
class Solution(object):
    def inorderSuccessor(self, root, p):
        """
        :type root: TreeNode
        :type p: TreeNode
        :rtype: TreeNode
        """
        # non-recursion
        if not root or not p:
            return None
        successor = None
        while root != p:
            if root.val < p.val:
                root = root.right
            else:
                successor = root
                root = root.left
        root = root.right
        if not root:
            return successor
        while root.left:
            root = root.left
        return root
```



