Increasing Triplet Subsequence 解题报告

Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:

Return true if there existsi, j, k such that arr\[i\] &lt; arr\[j\] &lt; arr\[k\] given 0 ≤ i &lt; j &lt; k ≤ n - 1 else return false.

Your algorithm should run in O\(n\) time complexity and O\(1\) space complexity.

**Examples:**

Given`[1, 2, 3, 4, 5]`, return`true`.

Given`[5, 4, 3, 2, 1]`, return`false`.

Idea:

这个题乍一看也是Longest Increasing Subsequence的特殊情况，最后是判断最大长度是否大于等于3就OK了，但是这样的话稍微想想一定不是最优解。所以大胆猜测这个题的最优时间复杂度应该为O\(n\)如果题目没有提示的话

解法：用两个变量first second保存第一小和第二小的数

如果遍历到的数比second大直接返回true

如果遍历到的数比first小，改写first为当前的数，这里不动second因为后面如果来比second大的数可以跟之前被替换掉的数构成解

如果遍历到的数比first大，比second小，替换second

```
class Solution(object):
    def increasingTriplet(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        from sys import maxint
        first, second = maxint, maxint
        for i in xrange(len(nums)):
            if nums[i] > second:
                return True
            if nums[i] < first:
                first = nums[i]
            if nums[i] > first and nums[i] < second:
                second = nums[i]
        return False
```



