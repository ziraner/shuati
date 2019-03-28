Two Sum

Given an array of integers, return**indices**of the two numbers such that they add up to a specific target.

You may assume that each input would have**exactly**one solution, and you may not use thesameelement twice.

**Example:**  


```
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

Idea:

General Two Sum问题有两种常规解法：

1.sort + 2p\(异向双指针\)， 一般来说空间复杂度O\(nlogn\),时间复杂度O\(1\)。但是本题的空间复杂度为O\(n\)

```
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        if not nums:
            return [0, 0]
        new_nums = []
        for idx, num in enumerate(nums):
            new_nums.append([num, idx])
        new_nums.sort(key = lambda x: x[0])
        n = len(nums)
        i, j = 0, n - 1
        while i < j:
            val = new_nums[i][0] + new_nums[j][0]
            if val < target:
                i += 1
            elif val > target:
                j -= 1
            else:
                return sorted([new_nums[i][1], new_nums[j][1]])
        return [0, 0]
```

2.hash。空间复杂度O\(n\)，时间复杂度O\(n\)

```
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hm, n = {}, len(nums)
        for i in xrange(n):
            diff = target - nums[i]
            if diff in hm:
                return sorted([i, hm[diff]])
            hm[nums[i]] = i
        return [0, 0]
```



