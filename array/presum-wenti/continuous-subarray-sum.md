Continuous Subarray Sum解题报告

Given a list of **non-negative** numbers and a target **integer** k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of **k**, that is, sums up to n\*k where n is also an **integer**.

**Example 1:**

```
Input: [23, 2, 4, 6, 7],  k=6

Output: True

Explanation: Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
```

**Example 2:**

```
Input: [23, 2, 6, 4, 7],  k=6

Output: True

Explanation: Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
```

**Note:**

1. The length of the array won't exceed 10,000.
2. You may assume the sum of all the numbers is in the range of a signed 32-bit integer.

Idea：

这个题目考察presum数组。值得注意的地方在语edge case的讨论。
1. k是0以及k不是0
2. 满足条件的长度要大于等于2

讨论k：
如果k为0，则简化为subarray sum， 注意讨论长度即可
如果k不为0，则根据mod的特性，如果两个presum对k的模一致则该位置之间的数相加必是k的倍数，所以只需要把presum mod k做为key存进hashmap即可

1. Python
```python
class Solution(object):
    def checkSubarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        hm = {0 : -1}
        presum = 0
        for i in xrange(len(nums)):
            presum += nums[i]
            tmp = presum
            if k != 0:
                tmp = presum % k
            if tmp in hm and i - hm[tmp] >= 2:
                return True
            if tmp not in hm:
                hm[tmp] = i
        return False
```
2. Java
```Java
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
        if (nums == null || nums.length < 2) {
            return false;
        }
        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        int presum = 0;
        for (int i = 0; i < nums.length; i++) {
            presum += nums[i];
            int num = presum;
            if (k != 0) {
                num %= k;
            }
            if (map.containsKey(num) && i - map.get(num) >= 2) {
                return true;
            } else if (!map.containsKey(num)) {
                map.put(num, i);
            }
        }
        return false;
    }
}
```
