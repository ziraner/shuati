Combination Sum II 解题报告

Given a collection of candidate numbers \(_C_\) and a target number \(_T_\), find all unique combinations in_C\_where the candidate numbers sums to\_T_.

Each number in\_C\_may only be used once in the combination.

Notice

* All numbers \(including target\) will be positive integers.
* Elements in a combination \(a1,\_a\_2, … ,\_a\_k\) must be in non-descending order. \(ie,\_a\_1≤\_a\_2≤ … ≤ak\).
* The solution set must not contain duplicate combinations.

```
class Solution:    
    """
    @param candidates: Given the candidate numbers
    @param target: Given the target number
    @return: All the combinations that sum to target
    """
    def combinationSum2(self, candidates, target): 
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
            self.dfs(candidates, target - candidates[i], i + 1, comb, result)
            comb.pop()
```



