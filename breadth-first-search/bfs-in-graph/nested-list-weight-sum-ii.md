Nested List Weight Sum II解题报告

Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

Different from the[previous question](https://leetcode.com/problems/nested-list-weight-sum/)where weight is increasing from root to leaf, now the weight is defined from bottom up. i.e., the leaf level integers have weight 1, and the root level integers have the largest weight.

**Example 1:**  
Given the list`[[1,1],2,[1,1]]`, return**8**. \(four 1's at depth 1, one 2 at depth 2\)

**Example 2:**  
Given the list`[1,[4,[6]]]`, return**17**. \(one 1 at depth 3, one 4 at depth 2, and one 6 at depth 1; 1\*3 + 4\*2 + 6\*1 = 17\)

Idea:

方法一：

递归，带着当前层的depth，和当前层integer和的数组

```
class Solution(object):
    def depthSumInverse(self, nestedList):
        """
        :type nestedList: List[NestedInteger]
        :rtype: int
        """
        if not nestedList:
            return 0
        lvl_sum = []
        self.dfs(nestedList, lvl_sum, 1)
        depth, ans = len(lvl_sum), 0
        for i in xrange(depth):
            ans += (depth - i) * lvl_sum[i]
        return ans

    def dfs(self, nestedList, lvl_sum, depth):
        if len(lvl_sum) < depth:
            lvl_sum.append(0)
        for nestedI in nestedList:
            if nestedI.isInteger():
                lvl_sum[depth - 1] += nestedI.getInteger()
            else:
                self.dfs(nestedI.getList(), lvl_sum, depth + 1)
```

方法二：

level order bfs，每次向下遍历一个level就把前一个level的和再加一遍

```
class Solution(object):
    def depthSumInverse(self, nestedList):
        """
        :type nestedList: List[NestedInteger]
        :rtype: int
        """
        q = []
        lvl_sum = []
        for nestedI in nestedList:
            q.append(nestedI)
            
        while q:
            size = len(q)
            cur_sum = 0
            for i in xrange(size):
                tmp = q.pop(0)
                if tmp.isInteger():
                    cur_sum += tmp.getInteger()
                else:
                    for nestedI in tmp.getList():
                        q.append(nestedI)
            lvl_sum.append(cur_sum)
        n = len(lvl_sum)
        ans = 0
        for i in xrange(n):
            ans += (n - i) * lvl_sum[i]
        return ans 
```



