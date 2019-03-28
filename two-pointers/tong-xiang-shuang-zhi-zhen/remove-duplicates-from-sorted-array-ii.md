Remove Duplicates from Sorted Array II 解题报告

Follow up for "Remove Duplicates":  
What if duplicates are allowed at mosttwice?

For example,  
Given sorted arraynums=`[1,1,1,2,2,3]`,

Your function should return length =`5`, with the first five elements ofnumsbeing`1`,`1`,`2`,`2`and`3`. It doesn't matter what you leave beyond the new length.

Idea:

是Remove Duplicates from Sorted Array的follow-up，用一个计数器cnt 数数

```
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        i, j, cnt = 0, 1, 1
        while j < len(nums):
            if nums[i] == nums[j] and cnt == 1:
                i += 1
                nums[i] = nums[j]
                cnt = 2
            elif nums[i] != nums[j]:
                i += 1
                nums[i] = nums[j]
                cnt = 1
            j += 1
        return i + 1
```



