Contiguous Array 解题报告

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**

```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**

```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

Idea:

是preSum: continuous number sum is zero的特殊情况。
可以将0看成-1，遇到0的时候presum -1，遇到1的时候presum +1；则问题转换成continuous number sum is zero.
用一hashmap保存之前出现过的presum值。如果遇到相同值，则更新ans；遇到不同的值将值和index存进map。

**Solution**
1. python
```python
class Solution(object):
    def findMaxLength(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        hm, presum = {0: -1}, 0
        ans = 0
        for i in xrange(len(nums)):
            if nums[i] == 1: presum += 1
            else: presum -= 1
            if presum in hm:
                ans = max(ans, i - hm[presum])
            else:
                hm[presum] = i
        return ans
```

2. java
```java
public class Solution {
    /**
     * @param nums: a binary array
     * @return: the maximum length of a contiguous subarray
     */
    public int findMaxLength(int[] nums) {
        // Write your code here
        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        int ans = 0;
        int preSum = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                preSum--;
            } else {
                preSum++;
            }
            if (map.containsKey(preSum)) {
                ans = Math.max(ans, i - map.get(preSum));
            } else {
                map.put(preSum, i);
            }
        }
        return ans;
    }
}
```
