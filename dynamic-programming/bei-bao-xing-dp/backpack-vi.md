Backpack VI\(Lintcode\) / Combination Sum IV\(Leetcode\)解题报告

Given an integer array`nums`with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer`target`.

##### Notice

A number in the array can be used multiple times in the combination.  
Different orders are counted as different combinations.

**Example**

Given nums =`[1, 2, 4]`, target =`4`

```
The possible combination ways are:
[1, 1, 1, 1]
[1, 1, 2]
[1, 2, 1]
[2, 1, 1]
[2, 2]
[4]
```

return`6`

因为又是无限次背包问题  
这个题区别于之前的背包问题，思路是先循环target，再循环数组中前j个数

dp\[i\] = sum\(dp\[i - nums\[j - 1\]\) if i &gt;= nums\[j - 1\]

```
dp[i] = sum(dp[i - nums[j - 1]])，其中i - nums[j] >= 0， i是背包当前容量，j是当前遍历到前多少个数class Solution:
    """
    @param: nums: an integer array and all positive numbers, no duplicates
    @param: target: An integer
    @return: An integer
    """
    def backPackVI(self, nums, target):
        # write your code here
        # BackPack IV is combination version
        # BackPack VI is permutation version
        # [1, 1, 2] and [1, 2, 1] and [2, 1, 1] are different
        # looping i from 0 to target first
        n = len(nums)
        f = [0 for _ in range(target + 1)]
        f[0] = 1
        for i in xrange(1, target + 1):
            for j in xrange(1, n + 1):
                if i >= nums[j - 1]:
                    f[i] += f[i - nums[j - 1]]
        return f[target]
```



