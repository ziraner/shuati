Maximum Average Subarray I 解题报告

Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.

**Example:**
```
Input: [1,12,-5,-6,50,3], k = 4
Output: 12.75
Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75
```

**Note:**
```
1 <= k <= n <= 30,000.
Elements of the given array will be in the range [-10,000, 10,000].
```

Idea:
Sliding Window题目不算是一个典型的presum问题。需要注意max只能在window的length等于k的时候被改写。

Solution:

```Java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int max = Integer.MIN_VALUE;
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (i >= k) {
                sum -= nums[i - k];
                max = Math.max(max, sum);
            } else {
                // to avoid max is kept to an invalid high value
                max = sum;
            }
        }
        return (double) max / k;
    }
}
```
