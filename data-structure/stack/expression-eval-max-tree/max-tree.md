Max Tree解题报告

Given an integer array with no duplicates. A max tree building on this array is defined as follow:

* The root is the maximum number in the array
* The left subtree and right subtree are the max trees of the subarray divided by the root number.

Construct the max tree by the given array.

**Example**

Given`[2, 5, 6, 0, 3, 1]`, the max tree constructed by this array is:

```
    6
   / \
  5   3
 /   / \
2   0   1
```

Idea

经典的maxtree构造问题，maxtree就是root是树里最大的，然后递归到subtree一直到最后

也利用单调栈的姿势。维护一个单调递减栈。如果来了个小B数b，则直接append到栈里，且将b做栈中最后一个数（如果存在的话）的右儿子；如果来了一个较大的数a，跟栈中最后一个数比较，如果a大，则循环pop直到stack为空或者stack中最后一个数大于a，pop的过程中不断的改写a.left = stack.pop\(\)，因为中间节点它们都是有一个root的，所以不怕pop没。

需要注意的地方是stack里面最后一个数如果小于等于当前的数的话也要pop

```
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""


class Solution:
    """
    @param: A: Given an integer array with no duplicates.
    @return: The root of max tree.
    """
    def maxTree(self, A):
        # write your code here
        stack = []
        for ele in A:
            node = TreeNode(ele)
            while stack and stack[-1].val <= node.val:
                node.left = stack.pop()
            if stack:
                stack[-1].right = node
            stack.append(node)
        if stack:
            return stack[0]
        return None
```



