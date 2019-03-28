Next Permutation 解题报告

Given a list of integers, which denote a permutation.

Find the next permutation in ascending order.

##### Notice

The list may contains duplicate integers.

**Example**

For`[1,3,2,3]`, the next permutation is`[1,3,3,2]`

For`[4,3,2,1]`, the next permutation is`[1,2,3,4]`

思路

引用自：http://fisherlei.blogspot.com/2012/12/leetcode-next-permutation.html

![](http://4.bp.blogspot.com/-4zN0u5JG0vs/UN0xPEkP5yI/AAAAAAAAG9Q/O48ZfwB1i_c/s1600/Picture4.png)

```
class Solution:
    """
    @param: nums: A list of integers
    @return: A list of integers
    """
    def nextPermutation(self, nums):
        # write your code here
        n = len(nums)
        i = n - 2
        while i != -1:
            if nums[i + 1] > nums[i]:
                break
            i -= 1
        if i == -1:
            return nums[::-1]
        for j in range(n - 1, i, -1):
            if nums[j] > nums[i]:
                nums[i], nums[j] = nums[j], nums[i]
                break
        return nums[:i + 1] + nums[i + 1:][::-1]

```



