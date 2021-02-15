Maximum Sum of 3 Non-Overlapping Subarrays 解题报告

In a given array`nums`of positive integers, find three non-overlapping subarrays with maximum sum.

Each subarray will be of size`k`, and we want to maximize the sum of all`3*k`entries.

Return the result as a list of indices representing the starting position of each interval \(0-indexed\). If there are multiple answers, return the lexicographically smallest one.

**Example:**

```
Input:[1,2,1,2,6,7,5,1], 2
Output: [0, 3, 5]
Explanation:
Subarrays [1, 2], [2, 6], [7, 5] correspond to the starting indices [0, 3, 5].
We could have also taken [2, 1], but an answer of [1, 3, 5] would be lexicographically larger.
```

**Note:**

`nums.length`will be between 1 and 20000.

`nums[i]`will be between 1 and 65535.

`k`will be between 1 and floor\(nums.length / 3\).

Idea:

1. 构造一个以K为window的sum数组wd\_sum
2. 原问题简化为：在wd\_sum数组中找三个数，它们之间的idx距离最小为i - j = k，使得这三个数和最大。解法跟maximum subarray II类似，开两个left，right数组，保存从左、右到该位置最大的值和idx；扫描i从k到len\(wdsum\) - k，找上述所说相隔idx最大的三个数的和。

```
class Solution(object):
    def maxSumOfThreeSubarrays(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        from sys import maxint
        n = len(nums)
        wd_sum = []
        preSum = 0
        for i in xrange(n):
            preSum += nums[i]
            if i >= k:
                preSum -= nums[i - k]
            if i >= k - 1:
                wd_sum.append(preSum)
        m = len(wd_sum)
        left = []
        right = []
        maxSum, maxIdx = -maxint, -1
        for i in xrange(m):
            if maxSum < wd_sum[i]:
                maxSum, maxIdx = wd_sum[i], i
            left.append([maxSum, maxIdx])
        maxSum, maxIdx = -maxint, -1
        for i in xrange(m - 1, -1, -1):
            if maxSum < wd_sum[i]:
                maxSum, maxIdx = wd_sum[i], i
            right.append([maxSum, maxIdx])
        right = right[::-1]
        maxSum, ans = -maxint, [-1, -1, -1]
        for i in xrange(k, m - k):
            val = left[i - k][0] + wd_sum[i] + right[i + k][0]
            if val > maxSum:
                maxSum, ans = val, [left[i -k][1], i, right[i + k][1]]
        return ans
```



