Longest Consecutive Sequence 解题报告

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example, Given`[100, 4, 200, 1, 3, 2]`, the longest consecutive elements sequence is`[1, 2, 3, 4]`. Return its length:`4`.

Your algorithm should run in O\(n\) complexity.

Idea:

这个题目和[Longest Increasing Subsequence](/dp/jie-long-xing-dp/longest-increasing-subsequence.md)/[Longest Continuous Increasing Subsequence](/dp/jie-long-xing-dp/longest-continuous-increasing-subsequence.md)在名字上很像，但是是不同的题目。

题目要求O\(n\)所以不能排序挨个走，用hashset把每个数存进去，然后走一遍数组，对每一个数往左往右走，走过的数都删掉，这样每一个数只会被遍历一次，时间复杂度O\(n\)。

往左往右走跟K Closest Numbers In Sorted Array挺像的

```
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        s = set([])
        for num in nums:
            s.add(num)
        ans = 0
        for i in xrange(len(nums)):
            if nums[i] in s:
                num = nums[i]
                s.remove(num)
            l, r = num - 1, num + 1
            while l in s:
                s.remove(l)
                l -= 1
            while r in s:
                s.remove(r)
                r += 1
            ans = max(ans, r - l - 1)
        return ans
```



