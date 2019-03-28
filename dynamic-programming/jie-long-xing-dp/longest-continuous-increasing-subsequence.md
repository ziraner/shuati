Leetcode: Longest Continuous Increasing Subsequence 解题报告

Given an unsorted array of integers, find the length of longest`continuous`increasing subsequence.

**Example 1:**

```
Input: [1,3,5,4,7]

Output: 3

Explanation: The longest continuous increasing subsequence is [1,3,5], its length is 3. 
Even though [1,3,5,7] is also an increasing subsequence, it's not a continuous one where 5 and 7 are separated by 4.
```

**Example 2:**

```
Input: [2,2,2,2,2]

Output: 1

Explanation: The longest continuous increasing subsequence is [2], its length is 1.
```

**Note:**Length of the array will not exceed 10,000.

Idea: 乍一看跟Longest Increasing Subsequence很像，但是要比那个简单，因为题目要求元素之间都是continuous的。所以猜测时间复杂度是O\(n\)

解法：保存一个变量length统计到当前index最长的length是多少，然后每次都更新下ans

```
class Solution(object):
    def findLengthOfLCIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        ans, length = 1, 1
        for i in xrange(1, len(nums)):
            if nums[i] > nums[i - 1]:
                length += 1
            else:
                length = 1
            ans = max(ans, length)
        return ans
```

Lintcode: Longest Increasing Continuous Subsequence

Give an integer array，find the longest increasing continuous subsequence in this array.

An increasing continuous subsequence:

* Can be from right to left or from left to right.
* Indices of the integers in the subsequence should be continuous.

##### Notice

O\(n\) time and O\(1\) extra space.

**Example**

For`[5, 4, 2, 1, 3]`, the LICS is`[5, 4, 2, 1]`, return`4`.

For`[5, 1, 2, 3, 4]`, the LICS is`[1, 2, 3, 4]`, return`4`.

Idea:

Lintcode 这个题目是leetcode的题目的double版，从左向右再从右向左扫两边array

```
class Solution:
    """
    @param: A: An array of Integer
    @return: an integer
    """
    def longestIncreasingContinuousSubsequence(self, A):
        # write your code here
        if not A:
            return 0
        n = len(A)
        ans, length = 1, 1
        for i in range(1, n):
            if A[i] > A[i - 1]:
                length += 1
            else:
                length = 1
            ans = max(length, ans)
        length = 1
        for i in range(n - 2, -1, -1):
            if A[i] > A[i + 1]:
                length += 1
            else:
                length = 1
            ans = max(length, ans)
        return ans
```



