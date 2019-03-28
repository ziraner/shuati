Minimum Size Subarray Sum解题报告

Given an array of**n**positive integers and a positive integer**s**, find the minimal length of a**contiguous**subarray of which the sum ≥**s**. If there isn't one, return 0 instead.

For example, given the array`[2,3,1,2,4,3]`and`s = 7`,  
the subarray`[4,3]`has the minimal length under the problem constraint.

[click to show more practice.](https://leetcode.com/problems/minimum-size-subarray-sum/description/#)

**More practice:**

If you have figured out theO\(n\) solution, try coding another solution of which the time complexity isO\(nlogn\).

Idea

同向双指针O\(n\)

```
class Solution(object):
    def minSubArrayLen(self, s, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """
        i, j, n = 0, 0, len(nums)
        presum, ans = 0, n + 1
        while j < n:
            while j < n and presum < s:
                presum += nums[j]
                j += 1
            while i < j and presum >= s:
                ans = min(ans, j - i)
                presum -= nums[i]
                i += 1
        if ans == n + 1:
            return 0
        return ans
```

二分答案O\(nlogn\)

```
class Solution(object):
    def minSubArrayLen(self, s, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        start, end = 0, n
        while start + 1 < end:
            mid = (start + end) / 2
            if self.check(nums, mid, s):
                end = mid
            else:
                start = mid
        if self.check(nums, start, s):
            return start
        if self.check(nums, end, s):
            return end
        return 0
    def check(self, nums, length, s):
        presum = 0
        for i in xrange(len(nums)):
            presum += nums[i]
            if i >= length:
                presum -= nums[i - length]
            if i + 1 >= length:
                if presum >= s:
                    return True
        return False 
```



