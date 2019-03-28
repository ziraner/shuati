Largest Divisible Subset解题报告

Given a set of`distinct positive`integers, find the largest subset such that every pair`(Si, Sj)`of elements in this subset satisfies:`Si % Sj = 0`or`Sj % Si = 0`.  
Notice

If there are multiple solutions, return any subset is fine.

**Example**

Given nums =`[1,2,3]`, return`[1,2]`or`[1,3]`

Given nums =`[1,2,4,8]`, return`[1,2,4,8]`

Idea:

这个题目先理解题意，如果可以构成这样一个subset意味着数组里面两两都是divisible的所以，我们找到他们的方式一定是从小到大排列，后面一个数是之前一个数的倍数。所以这个题要先sort。

其次这个题是一道比较难的接龙型DP的题目，题目让我们返回一个答案既可，所以可以用DP。但是因为返回的是答案而不是最长的子序列的长度，所以还是比较麻烦的，我们需要用一个prev数组保存和当前节点i构成最长divisible subset的之前一位是什么。然后因为有了maxlength和前一位idx的数组我们可以遍历一遍找到所有的数。

```
class Solution(object):
    def largestDivisibleSubset(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if not nums:
            return []
        n = len(nums)
        f = [1 for _ in xrange(n)]
        prev = [i for i in xrange(n)]
        nums.sort()
        for i in xrange(1, n):
            for j in xrange(i):
                if nums[i] % nums[j] == 0 and f[i] < f[j] + 1:
                    f[i] = f[j] + 1
                    prev[i] = j
        idx, maxLength = -1, -1
        for i in xrange(n):
            if f[i] > maxLength:
                idx, maxLength = i, f[i]
        ans = []
        for i in xrange(maxLength):
            ans.append(nums[idx])
            idx = prev[idx]
        return ans[::-1]
```



