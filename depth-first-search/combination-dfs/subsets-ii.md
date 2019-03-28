Subsets II 解题报告

Given a collection of integers that might contain duplicates,**nums**, return all possible subsets \(the power set\).

**Note:**The solution set must not contain duplicate subsets.

For example,  
If**nums**=`[1,2,2]`, a solution is:

```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

idea:

需要剪枝，如果两个数相同则只考虑第一个不考虑第二个。这样的话需要原数组排好序所以要先排序在dfs

```
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        subset, ans = [], []
        nums.sort()
        self.helper(nums, 0, subset, ans)
        return ans
    def helper(self, nums, pos, subset, ans):
        ans.append(subset[:])
        for i in xrange(pos, len(nums)):
            if i != pos and nums[i] == nums[i - 1]:
                continue
            subset.append(nums[i])
            self.helper(nums, i + 1, subset, ans)
            subset.pop()
```



