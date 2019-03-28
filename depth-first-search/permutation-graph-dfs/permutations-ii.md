Permutations II 解题报告

Given a list of numbers with duplicate number in it. Find all**unique**permutations.

**Example**

For numbers`[1,2,2]`the unique permutations are:

```
[
  [1,2,2],
  [2,1,2],
  [2,2,1]
]

```



```
class Solution:
    """
    @param nums: A list of integers.
    @return: A list of unique permutations.
    """
    def permuteUnique(self, nums):
        # write your code here
        perm = []
        result = []
        visited = [0 for _ in range(len(nums))]
        nums = sorted(nums)
        self.dfs(nums, perm, result, visited)
        return result

    def dfs(self, nums, perm, result, visited):
        if len(nums) == len(perm):
            result.append(perm[:])
            return
        for i in range(len(nums)):
            if visited[i]:
                continue
            if i != 0 and nums[i] == nums[i - 1] and visited[i - 1] == 0:
                continue
            visited[i] = 1
            perm.append(nums[i])
            self.dfs(nums, perm, result, visited)
            visited[i] = 0
            perm.pop()



```



