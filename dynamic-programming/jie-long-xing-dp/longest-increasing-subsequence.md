Longest Increasing Subsequence 解题报告

Given an unsorted array of integers, find the length of longest increasing subsequence.

For example, Given`[10, 9, 2, 5, 3, 7, 101, 18]`,  
The longest increasing subsequence is`[2, 3, 7, 101]`, therefore the length is`4`. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O\(n2\) complexity.

**Follow up:**Could you improve it to O\(nlogn\) time complexity?

Idea:

O\(n^2\)的时间复杂度：

接龙型DP，f\[i\]表示到下标为i的位置，从前面任意一点过来所组成的longest increasing subsequence的长度。

```
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        n = len(nums)
        f = [1 for _ in xrange(n)]
        for i in xrange(1, n):
            for j in xrange(i):
                if nums[j] < nums[i]:
                    f[i] = max(f[i], f[j] + 1)
        return max(f)
```

O\(nlogn\):

二分法

原数组不是有序的，没法二分，我们需要构造一个有序的可以二分的数组，这个时候想到了单调栈类似的思路：构造一个类似于单调栈的数组，对nums数组每进来一个数，通过二分查找，找到第一个大于等于该数的idx，然后替换掉该idx的原来的数。这个数组和单调栈的区别是，单调栈弹出之前所有的元素，而这个数组只改写查找到idx上面的数。

最后扫一遍有序数组，从后面找第一个不是maxint的数就是所求的idx 因为题目求长度，所以需要返回idx + 1

```
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        n = len(nums)
        # O(nlogn)
        from sys import maxint
        f = [maxint for _ in xrange(n)]
        idx = n - 1
        for i in xrange(n):
            idx = self.binarySearch(f, nums[i])
            f[idx] = nums[i]
        for i in xrange(n - 1, -1, -1):
            if f[i] != maxint:
                break
        return i + 1
    def binarySearch(self, f, num):
        start, end = 0, len(f) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if f[mid] > num:
                end = mid
            else:
                start = mid
        if f[start] >= num:
            return start
        return end
```



