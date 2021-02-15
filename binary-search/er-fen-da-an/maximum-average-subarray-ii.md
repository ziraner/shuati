Maximum Average Subarray II

**Problem:**

Given an array with positive and negative numbers, find the `maximum average subarray` which length should be greater or equal to given length`k`.

**Notice**

It's guaranteed that the size of the array is greater or equal to _k_.

**Example**

Given nums =`[1, 12, -5, -6, 50, 3]`, k =`3`

Return`15.667`// \(-6 + 50 + 3\) / 3 = 15.667

**Idea:**

二分答案，因为所求的解一定是要大于数组中最小的数，小于数组中最大的数。所以可以用精度二分答案来解。对于每个提出的答案数值，进行可行解判断。

可行解判断：判断是否存在一个subarray，使得平均和大于等于当前可行解，转化为先将原来数组每个值都减去可行解，然后是否存在length &gt;= k的subarray使得subarray最大的和>=0，是一道max subarray问题。

Solution:

```python
from sys import maxint

class Solution:
    # @param {int[]} nums an array with positive and negative numbers
    # @param {int} k an integer
    # @return {double} the maximum average
    def maxAverage(self, nums, k):
        # Write your code here
        start, end = min(nums), max(nums)
        error = 1e-6
        while start + error < end:
            mid = (start + end) / 2.0
            if self.check(mid, nums, k):
                start = mid
            else:
                end = mid
        return start
    # this is similar to maximum subarray IV
    def check(self, ans, nums, k):
        min_pre = 0
        n = len(nums)
        preSum = [0 for _ in range(n + 1)]
        for i in range(1, n + 1):
            preSum[i] = nums[i - 1] + preSum[i - 1] - ans
            if i >= k and preSum[i] - min_pre >= 0:
                return True
            if i >= k:
                min_pre = min(min_pre, preSum[i - k + 1])
        return False

```

2. Java
```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int minValue = Integer.MAX_VALUE;
        int maxValue = Integer.MIN_VALUE;
        for (int num: nums) {
            minValue = Math.min(minValue, num);
            maxValue = Math.max(maxValue, num);
        }
        double start = minValue;
        double end = maxValue;
        double ERROR = 1e-5;
        while (start + ERROR < end) {
            double mid = (start + end) / 2;
            if (isValid(mid, nums, k)) {
                start = mid;
            } else {
                end = mid;
            }
        }
        return start;
    }

    private boolean isValid(double avgValue, int[] nums, int k) {
        // O(1) space complexity
        // preSum is the current preSum at i
        // leftPreSum is the current preSum at i - k
        // minLeftPreSum is the min of preSum from 0 to i - k
        double preSum = 0;
        double leftPreSum = 0;
        double minLeftPreSum = 0;
        for (int i = 0; i < nums.length; i++) {
            preSum += nums[i] - avgValue;
            // if the first 4 numbers: minLeftPreSum is initialized to 0 already
            if (i >= k) {
                leftPreSum += nums[i - k] - avgValue;
                minLeftPreSum = Math.min(minLeftPreSum, leftPreSum);
            }
            // the first 4 numbers is ok
            if (i >= k - 1 && preSum - minLeftPreSum >= 0) {
                return true;
            }
        }
        return false;
    }
}
```
