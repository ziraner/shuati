Number of Longest Increasing Subsequence解题报告

Given an unsorted array of integers, find the number of longest increasing subsequence.

**Example 1:**

```
Input: [1,3,5,4,7]

Output: 2

Explanation: 
The two longest increasing subsequence are [1, 3, 4, 7] and [1, 3, 5, 7].
```

**Example 2:**

```
Input: [2,2,2,2,2]

Output: 5

Explanation: 
The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```

**Note: **Length of the given array will be not exceed 2000 and the answer is guaranteed to be fit in 32-bit signed int.

Idea:

这个题是LIS的加强版

定义两个数组f就是LIS里的数组,cnt为当前idx LIS的数目

if 组成一个更长的长度：cnt\[i\] = cnt\[j\]

elif 长度跟当前长度相同：cnt\[i\] += cnt\[j\]

```
class Solution(object):
    def findNumberOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        n = len(nums)
        f = [1 for _ in xrange(n)]
        cnt = [1 for _ in xrange(n)]
        for i in xrange(1, n):
            for j in xrange(i):
                if nums[j] < nums[i]:
                    if f[i] <= f[j]:
                        f[i] = f[j] + 1
                        cnt[i] = cnt[j]
                    elif f[i] == f[j] + 1:
                        cnt[i] += cnt[j]
        max_f = max(f)
        ans = 0
        for i in xrange(n):
            if f[i] == max_f:
                ans += cnt[i]
        return ans
```



