Random Pick Index 解题报告

Given an array of integers with possible duplicates, randomly output the index of a given target number. You can assume that the given target number must exist in the array.

**Note:**  
The array size can be very large. Solution that uses too much extra space will not pass the judge.

**Example:**

```
int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
solution.pick(3);

// pick(1) should return 0. Since in the array only nums[0] is equal to 1.
solution.pick(1);
```

Idea: 

reservoir sampling, 扫描数组，对于每一个等于target的数选择它的概率是1/cnt，cnt为当前等于target的数的数量。

```
class Solution(object):

    def __init__(self, nums):
        """
        
        :type nums: List[int]
        :type numsSize: int
        """
        self.numbers = nums

    def pick(self, target):
        """
        :type target: int
        :rtype: int
        """
        from random import random
        idx, cnt = 0, 0
        for i in xrange(len(self.numbers)):
            if target == self.numbers[i]:
                cnt += 1
                if random() < 1.0 / cnt:
                    idx = i
        return idx


# Your Solution object will be instantiated and called as such:
# obj = Solution(nums)
# param_1 = obj.pick(target)
```



