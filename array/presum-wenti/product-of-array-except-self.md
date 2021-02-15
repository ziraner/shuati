Product of Array Except Self 解题报告

Given an array of n integers where n &gt; 1:`nums`, return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

Solve it **without division **and in O\(n\).

For example, given`[1,2,3,4]`, return`[24,12,8,6]`.

**Follow up:**  
Could you solve it with constant space complexity? \(Note: The output array **does not** count as extra space for the purpose of space complexity analysis.\)

思路

题目要求

1.O\(n\) 2.不能用除法 3.除了返回答案的O\(n\) space之外不能另开空间

1.O\(n\)就想到了利用presum的概念，但是这里用的是premultiply。

2.不许用除法，就是不能只构造一个presum数组。这个题我们构造两个，一个从前向后一个从后向前

\[a1, a2, a3, a4\] ----&gt; forward: \[1, a1, a1\*a2, a1\*a2\*a3\] reverse:\[a2\*a3\*a4, a3\*a4, a4, 1\] -----&gt; forward \* reverse =

\[a2\*a3\*a4, a1\*a3\*a4, a1\*a3\*a4, a1\*a2\*a3\]即为所求

3.除了ans不允许开space，则需要把forward存进ans中，第二遍从后往前扫，只保存一个reverse变量既可

```python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        n = len(nums)
        ans = [1 for _ in xrange(n)]
        for i in xrange(1, n):
            ans[i] = ans[i - 1] * nums[i - 1]
        tmp = 1
        for i in xrange(n - 1, -1, -1):
            ans[i] *= tmp
            tmp *= nums[i]
        return ans
```
