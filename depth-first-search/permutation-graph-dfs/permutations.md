Permutations 解题报告

Given a list of numbers, return all possible permutations.

**Example**

For nums =`[1,2,3]`, the permutations are:

```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]

```

```
class Solution:
    """
    @param nums: A list of Integers.
    @return: A list of permutations.
    """
    def permute(self, nums):
        # write your code here
        perm = []
        result = []
        visited = [0 for _ in range(len(nums))]
        self.dfs(nums, perm, result, visited)
        return result

    def dfs(self, nums, perm, result, visited):
        if len(perm) == len(nums):
            result.append(perm[:])
            return
        for i in range(len(nums)):
            if visited[i]:
                continue
            visited[i] = 1
            perm.append(nums[i])
            self.dfs(nums, perm, result, visited)
            visited[i] = 0
            perm.pop()


```



