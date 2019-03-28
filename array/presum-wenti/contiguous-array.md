Contiguous Array 解题报告

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**

```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**

```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

Idea:

当遇到0 presum -1 当遇到1 presum +1

用一hashmap保存之前出现过的presum值，如果遇到相同值 更新ans；遇到不同值 加入hashmap

```
class Solution(object):
    def findMaxLength(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        hm, presum = {0: -1}, 0
        ans = 0
        for i in xrange(len(nums)):
            if nums[i] == 1: presum += 1
            else: presum -= 1
            if presum in hm:
                ans = max(ans, i - hm[presum])
            else:
                hm[presum] = i
        return ans
```



