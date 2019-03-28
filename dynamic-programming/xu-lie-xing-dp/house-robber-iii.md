House Robber III 解题报告

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

**Example**

```
  3
 / \
2   3
 \   \ 
  3   1

```

Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.

```
    3
   / \
  4   5
 / \   \ 
1   3   1

```

Maximum amount of money the thief can rob = 4 + 5 = 9.

思路：

divide and conquer，返回两个值，偷的话一共能偷多少，不偷的话一共能偷多少。

注意算not rob的时候不能思维定势，not rob的值是max\(left not rob, left rob\) + max\(r not rob, r rob\)。因为可以选择左边不rob和右边不rob。

```
class Solution:
    """
    @param: root: The root of binary tree.
    @return: The maximum amount of money you can rob tonight
    """
    def houseRobber3(self, root):
        # write your code here
        return max(self.dfs(root))
    def dfs(self, root):
        if not root:
            return 0, 0
        l_rob, l_not_rob = self.dfs(root.left)
        r_rob, r_not_rob = self.dfs(root.right)
        rob = l_not_rob + r_not_rob + root.val
        not_rob = max(l_not_rob, l_rob) + max(r_not_rob, r_rob)
        return rob, not_rob
```



