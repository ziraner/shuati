Sort Color 解题报告

Given an array withnobjects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:**  
You are not suppose to use the library's sort function for this problem.

[click to show follow up.](https://leetcode.com/problems/sort-colors/description/#)

**Follow up:**  
A rather straight forward solution is a two-pass algorithm using counting sort.  
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

Could you come up with an one-pass algorithm using only constant space?

Idea:

最简单的想法是count sorting

```
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        # counting sort
        zeros, ones, twos = 0, 0, 0
        for num in nums:
            if num == 0:
                zeros += 1
            elif num == 1:
                ones += 1
            else:
                twos += 1
        for i in xrange(len(nums)):
            if zeros > 0:
                nums[i] = 0
                zeros -= 1
            elif ones > 0:
                nums[i] = 1
                ones -= 1
            else:
                nums[i] = 2
                twos -= 1
```

因为follow-up不允许count sorting，所以两个指针（其实是三个指针，有同向有异向）

```
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        # two pointers
        n = len(nums)
        zero, one, two = 0, 0, n - 1
        while one <= two:
            if nums[one] == 0:
                nums[zero], nums[one] = nums[one], nums[zero]
                zero += 1
                one += 1
            elif nums[one] == 2:
                nums[one], nums[two] = nums[two], nums[one]
                two -= 1
            else:
                one += 1

```



