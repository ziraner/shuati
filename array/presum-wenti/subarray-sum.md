Subarray Sum

Given an integer array, find a subarray where the sum of numbers is zero. Your code should return the index of the first number and the index of the last number.

Example 1:
```
Input:  [-3, 1, 2, -3, 4]
Output: [0, 2] or [1, 3]
Explanation: return anyone that the sum is 0
```
Example 2:
```
Input:  [-3, 1, -4, 2, -3, 4]
Output: [1,5]
```

Idea:

这是一道经典的用presum的问题。
presum的一般解法：
用hashmap保存value -> index的映射；
一般来说index可以从-1开始，也可以从0开始，取决于对于presum的定义；
如果从0开始:
* 初始化的时候hashmap.put(0, -1)
* 在hashmap中找到了key相同的值则说明index在[i + 1, j]上面的数字加起来是0

Solution:

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    public List<Integer> subarraySum(int[] nums) {
        // write your code here
        HashMap<Integer, Integer> map = new HashMap<>();
        List<Integer> ans = new ArrayList<>();
        map.put(0, -1);
        int presum = 0;
        for (int i = 0; i < nums.length; i++) {
            presum += nums[i];
            if (map.containsKey(presum)) {
                ans.add(map.get(presum) + 1);
                ans.add(i);
                return ans;
            } else {
                map.put(presum, i);
            }
        }
        return ans;
    }
}
```
