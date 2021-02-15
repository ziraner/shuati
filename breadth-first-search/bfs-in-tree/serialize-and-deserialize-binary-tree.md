Serialize and Deserialize Binary Tree 解题报告

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

For example, you may serialize the following tree

```
    1
   / \
  2   3
     / \
    4   5
```

as`"[1,2,3,null,null,4,5]"`

Idea:

树中BFS，Serialize & Deserialize 都用Queue来做。

Serialize的循环条件是idx小于q的长度：这个判断条件有点tricky，因为一个循环里，q的长度要增加2而idx增加1；需要注意判断当前idx的元素是否为None，是的话idx直接+1；遍历完所有叶子节点后，q中最后会有很多空（叶子节点的左右子树），所以最后循环可以终止。循环终止之后要将最后的None pop掉，然后在写成string的形式

deserialize跟serialize类似，idx要对应q中两个元素，所以需要一个flag变量去判断当前的值应该插入idx的左子树还是右子树。tricky的地方在于，如果当前元素是None，则不要进q，对应更改idx就可以。

最后不要忘了corner case root 为空需要单独判断

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return '[]'
        i, q = 0, [root]
        while i < len(q):
            if q[i]:
                q.append(q[i].left)
                q.append(q[i].right)
            i += 1
        while not q:
            q.pop()
        ans = []
        for i in xrange(len(q)):
            if q[i]:
                ans.append(str(q[i].val))
            else:
                ans.append('#')
        return '[' + ','.join(ans) + ']'

    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        if data == '[]':
            return None
        vals = data.strip().strip('[').strip(']').split(',')
        i, isLeft, q = 0, True, [TreeNode(int(vals.pop(0)))]
        for val in vals:
            node = None
            if val != '#':
                node = TreeNode(int(val))
                q.append(node)
            if isLeft:
                q[i].left = node
            else:
                q[i].right = node
            if not isLeft:
                i += 1
            isLeft = not isLeft
        return q[0]
# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```
