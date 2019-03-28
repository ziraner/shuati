Remove Duplicate Numbers in Array 解题报告

Given an array of integers, remove the duplicate numbers in it.

You should:  
1. Do it in place in the array.  
2. Move the unique numbers to the front of the array.  
3. Return the total number of the unique numbers.

##### Notice

You don't need to keep the original order of the integers.

**Example**

Given_nums_=`[1,3,1,4,4,2]`, you should:

1. Move duplicate integers to the tail of
   nums; nums=[1,3,4,2,?,?]
2. Return the number of unique integers in nums; 4

Actually we don't care about what you place in`?`, we only care about the part which has no duplicate integers.

Idea:

这个题原array是没有排序的，有两种方法。

方法一：哈希，时间复杂度O\(n\) 空间复杂度O\(n\)

```
class Solution:
    # @param {int[]} nums an array of integers
    # @return {int} the number of unique integers
    def deduplication(self, nums):
        # Write your code here
        # O(n) time
        h, i = set([]), 0
        for num in nums:
            if num not in h:
                h.add(num)
                nums[i] = num
                i += 1
        return i
```

方法二：先排序再两个指针：时间复杂度O\(nlog\)，空间复杂度O\(1\)
同向双指针i,j: i指向最后一个不重复的数，j遍历整个数组

```
class Solution:
    # @param {int[]} nums an array of integers
    # @return {int} the number of unique integers
    def deduplication(self, nums):
        # Write your code here
        if not nums:
            return 0
        nums.sort()
        i, j = 0, 1
        while j < len(nums):
            if nums[i] != nums[j]:
                i = i + 1
                nums[i] = nums[j]
            j += 1
        return i + 1
```



