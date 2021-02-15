Maximum Subarray II

Given an array of integers, find two non-overlapping subarrays which have the largest sum.  
The number in each subarray should be contiguous.  
Return the largest sum.

**Notice**

The subarray should contain at least one number

**Example**

For given`[1, 3, -1, 2, -1, 2]`, the two subarrays are`[1, 3]`and`[2, -1, 2]`or`[1, 3, -1, 2]`and`[2]`, they both have the largest sum`7`.

**Idea:**

是max subarray的扩展。O(1)的空间即三个preSum，minPreSum，maxSum变量是不够的；思路是从左到右构造一个int[] leftMaxSum，从右到左构造一个int[] rightMaxSum，然后对leftMaxSum[i] + rightMaxSum[i]挨位检查。

**Solution**
1. python
```python
class Solution:
    """
    @param: nums: A list of integers
    @return: An integer denotes the sum of max two non-overlapping subarrays
    """
    def maxTwoSubArrays(self, nums):
        # write your code here
        # left[]: maximum subarray sum from the left
        # right[]: maximum subarray sum from the right
        n = len(nums)
        from sys import maxint
        left = [0 for _ in xrange(n)]
        right = [0 for _ in xrange(n)]
        preSum, minSum = 0, 0
        tmp = -maxint
        for i in xrange(n):
            preSum += nums[i]
            tmp = max(tmp, preSum - minSum)
            minSum = min(preSum, minSum)
            left[i] = tmp
        preSum, minSum = 0, 0
        tmp = -maxint
        for i in xrange(n - 1, -1, -1):
            preSum += nums[i]
            tmp = max(tmp, preSum - minSum)
            minSum = min(preSum, minSum)
            right[i] = tmp
        ans = -maxint
        for i in xrange(1, n):
            ans = max(ans, left[i - 1] + right[i])
        return ans
```

2. java
```java
public class Solution {
    /*
     * @param nums: A list of integers
     * @return: An integer denotes the sum of max two non-overlapping subarrays
     */
    public int maxTwoSubArrays(List<Integer> nums) {
        // write your code here
        int length = nums.size();
        int[] leftMaxSum = new int[length];
        int[] rightMaxSum = new int[length];
        int minPreSum = 0;
        int preSum = 0;
        int maxSum = Integer.MIN_VALUE;
        for (int i = 0; i < length; i++) {
            preSum += nums.get(i);
            maxSum = Math.max(maxSum, preSum - minPreSum);
            minPreSum = Math.min(minPreSum, preSum);
            leftMaxSum[i] = maxSum;
        }
        minPreSum = 0;
        preSum = 0;
        maxSum = Integer.MIN_VALUE;
        for (int i = length - 1; i >= 0; i--) {
            preSum += nums.get(i);
            maxSum = Math.max(maxSum, preSum - minPreSum);
            minPreSum = Math.min(minPreSum, preSum);
            rightMaxSum[i] = maxSum;
        }
        maxSum = Integer.MIN_VALUE;
        for (int i = 0; i < length - 1; i++) {
            maxSum = Math.max(maxSum, leftMaxSum[i] + rightMaxSum[i + 1]);
        }
        return maxSum;
    }
}
```
