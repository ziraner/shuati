Lowest Common Ancestor 解题报告

Given the root and two nodes in a Binary Tree. Find the lowest common ancestor\(LCA\) of the two nodes.

The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.

##### Notice

Assume two nodes are exist in tree.

**Example**

For the following binary tree:

```
  4
 / \
3   7
   / \
  5   6
```

LCA\(3, 5\) =`4`

LCA\(5, 6\) =`7`

LCA\(6, 7\) =`7`

Idea:

helper 中判断返回顺序为：

root is None: return None

left is not None and right is not None or root is p or root is q: return root

left is not None: return left

right is not None: return right

return None

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        if not root:
            return None
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if left and right or root is p or root is q:
            return root
        if left:
            return left
        if right:
            return right
        return None
```

Follow-Up1:

##### Notice

node A or node B may not exist in tree.

这个follow-up需要return value为三个量：a是否存在当前树中，b是否存在当前树中，lca是什么

helper中的写法和顺序和原题一样

```
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
"""
class Solution:
    """
    @param root: The root of the binary search tree.
    @param A and B: two nodes in a Binary.
    @return: Return the least common ancestor(LCA) of the two nodes.
    """ 
    def lowestCommonAncestor3(self, root, A, B):
        # write your code here
        # need two more return values a and b to make sure if a and b are in the tree
        hasA, hasB, lca = self.helper(root, A, B)
        if hasA and hasB:
            return lca
        return None
    def helper(self, root, A, B):
        if not root:
            return False, False, None
        l_hasA, l_hasB, l_lca = self.helper(root.left, A, B)
        r_hasA, r_hasB, r_lca = self.helper(root.right, A, B)
        hasA = l_hasA or r_hasA or root is A
        hasB = l_hasB or r_hasB or root is B
        if root is A or root is B or l_lca and r_lca:
            return hasA, hasB, root
        if l_lca:
            return hasA, hasB, l_lca
        if r_lca:
            return hasA, hasB, r_lca
        return False, False, None
```

Follow-Up2:

Lowest Common Ancestor of a Binary Search Tree

直接通过比值就可以判断LCA在哪里

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        if not root:
            return None
        if root.val < p.val and root.val < q.val:
            return self.lowestCommonAncestor(root.right, p, q)
        if root.val > p.val and root.val > q.val:
            return self.lowestCommonAncestor(root.left, p, q)
        return root
```

Follow-Up3:

The node has an extra attribute`parent`which point to the father of itself. The root's parent is null.

有parent node使得这个题目变得更简单了，用一个hashset记录某一个点向上的路径既可。

```
"""
Definition of ParentTreeNode:
class ParentTreeNode:
    def __init__(self, val):
        self.val = val
        self.parent, self.left, self.right = None, None, None
"""
class Solution:
    """
    @param root: The root of the tree
    @param A and B: Two node in the tree
    @return: The lowest common ancestor of A and B
    """ 
    def lowestCommonAncestorII(self, root, A, B):
        # Write your code here
        hs = set([])
        while A:
            hs.add(A)
            A = A.parent
        while B:
            if B in hs:
                return B
            B = B.parent
        return None
```



