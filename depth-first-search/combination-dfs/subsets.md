Subsets 解题报告

Given a set of **distinct **integers,nums, return all possible subsets \(the power set\).

**Note:**The solution set must not contain duplicate subsets.

For example,  
If**nums**=`[1,2,3]`, a solution is:

```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

```
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        subset, ans = [], []
        self.helper(nums, 0, subset, ans)
        return ans
    def helper(self, nums, pos, subset, ans):
        ans.append(subset[:])
        for i in xrange(pos, len(nums)):
            subset.append(nums[i])
            self.helper(nums, i + 1, subset, ans)
            subset.pop()
```



