Maximum Subarray 解题报告

Find the contiguous subarray within an array \(containing at least one number\) which has the largest sum.

For example, given the array`[-2,1,-3,4,-1,2,1,-5,4]`,  
the contiguous subarray`[4,-1,2,1]`has the largest sum =`6`.

**Solution**
1. python
```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        preSum, minSum = 0, 0
        from sys import maxint
        ans = -maxint
        for num in nums:
            preSum += num
            ans = max(ans, preSum - minSum)
            minSum = min(preSum, minSum)
        return ans
```
2. java
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int preSum = 0;
        int minPreSum = 0;
        int maxSum = Integer.MIN_VALUE;
        for (int num : nums) {
            preSum += num;
            maxSum = Math.max(maxSum, preSum - minPreSum);
            minPreSum = Math.min(minPreSum, preSum);
        }
        return maxSum;
    }
}
```
