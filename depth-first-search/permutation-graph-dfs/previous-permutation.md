Previous Permutation解题报告

Given a list of integers, which denote a permutation.

Find the previous permutation in ascending order.

##### Notice

The list may contains duplicate integers.

  
**Example**

For`[1,3,2,3]`, the previous permutation is`[1,2,3,3]`

For`[1,2,3,4]`, the previous permutation is`[4,3,2,1]`

  
是next permutation的逆过程，所有的地方大于号和小于号对换就可以了

```
class Solution:
    """
    @param: nums: A list of integers
    @return: A list of integers that's previous permuation
    """
    def previousPermuation(self, nums):
        # write your code here
        n = len(nums)
        i = n - 2
        while i != -1:
            if nums[i + 1] < nums[i]:
                break
            i -= 1
        if i == -1:
            return nums[::-1]
        for j in range(n - 1, i, -1):
            if nums[j] < nums[i]:
                nums[j], nums[i] = nums[i], nums[j]
                break
        return nums[:i + 1] + nums[i + 1:][::-1]
```



