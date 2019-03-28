Nested List Weight Sum解题报告

Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

**Example 1:**  
Given the list`[[1,1],2,[1,1]]`, return**10**. \(four 1's at depth 2, one 2 at depth 1\)

**Example 2:**  
Given the list`[1,[4,[6]]]`, return**27**. \(one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4\*2 + 6\*3 = 27\)

Idea：

方法一：递归

```
class Solution(object):
    def depthSum(self, nestedList):
        """
        :type nestedList: List[NestedInteger]
        :rtype: int
        """
        return self.dfs(nestedList, 1)
    def dfs(self, nestedList, depth):
        if not nestedList:
            return 0
        ans = 0
        for nestedI in nestedList:
            if nestedI.isInteger():
                ans += depth * nestedI.getInteger()
            else:
                ans += self.dfs(nestedI.getList(), depth + 1)
        return ans
```

方法二：BFS level order traversal

```
class Solution(object):
    def depthSum(self, nestedList):
        """
        :type nestedList: List[NestedInteger]
        :rtype: int
        """
        q = []
        depth = 1
        for nestedI in nestedList:
            q.append(nestedI)
        ans = 0
        while q:
            size = len(q)
            for i in xrange(size):
                tmp = q.pop(0)
                if tmp.isInteger():
                    ans += tmp.getInteger() * depth
                else:
                    for nestedI in tmp.getList():
                        q.append(nestedI)
            depth += 1
        return ans

```

  


