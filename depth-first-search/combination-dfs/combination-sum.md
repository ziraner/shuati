Combination Sum 解题报告

Given a set of candidate numbers \(_**C**_\) and a target number \(_**T**_\), find all unique combinations in_**C**\_where the candidate numbers sums to_**T**\_.

The**same**repeated number may be chosen from\_**C**\_unlimited number of times.

Notice

* All numbers \(including target\) will be positive integers.
* Elements in a combination \(a1,\_a\_2, … ,\_a\_k\) must be in non-descending order. \(ie,\_a\_1≤\_a\_2≤ … ≤ak\).
* The solution set must not contain duplicate combinations.

```
class Solution:
    # @param candidates, a list of integers
    # @param target, integer
    # @return a list of lists of integers
    def combinationSum(self, candidates, target):
        # write your code here
        if not candidates or not target:
            return []

        result = []
        comb = []
        candidates = sorted(candidates)
        self.dfs(candidates, target, 0, comb, result)
        return result

    def dfs(self, candidates, target, startIndex, comb, result):
        if target == 0:
            result.append(comb[:])
            return

        for i in range(startIndex, len(candidates)):
            if target < candidates[i]:
                break
            if i != startIndex and candidates[i] == candidates[i - 1]:
                continue
            comb.append(candidates[i])
            self.dfs(candidates, target - candidates[i], i, comb, result)
            comb.pop()
```



