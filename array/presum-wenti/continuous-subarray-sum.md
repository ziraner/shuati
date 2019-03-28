Continuous Subarray Sum解题报告

Given a list of **non-negative **numbers and a target **integer **k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of **k**, that is, sums up to n\*k where n is also an **integer**.

**Example 1:**

```
Input: [23, 2, 4, 6, 7],  k=6

Output: True

Explanation: Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
```

**Example 2:**

```
Input: [23, 2, 6, 4, 7],  k=6

Output: True

Explanation: Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
```

**Note:**

1. The length of the array won't exceed 10,000.
2. You may assume the sum of all the numbers is in the range of a signed 32-bit integer.

Idea：

这个题目考察presum数组。如果k为0则找subarray sum是0的长度大于等于2的是否存在；如果k不为零，则presum对k取mod，找对k取mod相等的数。用一个hashmap存presum或presum mod k

```
class Solution(object):
    def checkSubarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        hm = {0 : -1}
        presum = 0
        for i in xrange(len(nums)):
            presum += nums[i]
            tmp = presum
            if k != 0:
                tmp = presum % k
            if tmp in hm and i - hm[tmp] >= 2:
                return True
            if tmp not in hm:
                hm[tmp] = i
        return False
```

  


