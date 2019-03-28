Two Sum - Input array is sorted 解题报告

Given an array of integers that is already_sorted in ascending order_, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers \(both index1 and index2\) are not zero-based.

##### Notice

You may assume that each input would have exactly one solution.

**Example**

Given nums =`[2, 7, 11, 15]`, target =`9`  
return`[1, 2]`

Idea:

Two Sum变种，用2P解

```
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        i, j = 0, len(numbers) - 1
        while i < j:
            val = numbers[i] + numbers[j]
            if val < target:
                i += 1
            elif val > target:
                j -= 1
            else:
                return [i + 1, j + 1]
        return [0, 0]
```



