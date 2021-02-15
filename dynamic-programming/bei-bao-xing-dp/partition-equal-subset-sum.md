Partition Equal Subset Sum 解题报告

Given a `non-empty` array containing `only positive integers`, find if the array can be partitioned into `two` subsets such that the sum of elements in both subsets is equal.

**Notice**

Each of the array element will not exceed 100.  
The array size will not exceed 200.

**Example**

Given nums =`[1, 5, 11, 5]`, return`true`  
two subsets: \[1, 5, 5\], \[11\]

Given nums =`[1, 2, 3, 9]`, return`false`

思路

backpack问题的变形，可以用滚动数组优化最后

```python
class Solution:
    """
    @param: nums: a non-empty array only positive integers
    @return: true if can partition or false
    """
    def canPartition(self, nums):
        # write your code here
        if not nums:
            return True
        if sum(nums) % 2 != 0:
            return False
        target = sum(nums) / 2
        n = len(nums)
        f = [[False for _ in xrange(target + 1)] for _ in xrange(n + 1)]
        f[0][0] = True
        for i in xrange(1, n + 1):
            for j in xrange(1, target + 1):
                if j >= nums[i - 1]:
                    f[i][j] = f[i - 1][j] or f[i - 1][j - nums[i - 1]]
                else:
                    f[i][j] = f[i - 1][j]
        return f[n][target]

```
