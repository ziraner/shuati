Presum相关问题：

PreSum相关问题有两种

1. continuous numbers sum is 0 or similar
  * 这类问题本质上跟Two Sum问题类似。都是需要一个hashmap，过一遍数组可以在O(n)时间内解决问题。
  * Two Sum的hashmap的key是target - nums[i], value是index Presum的hashmap的key可以是presum[i], value是index或index + 1.
2. max continuous numbers sum or similar
  * 这类问题除了preSum之外还需要记住minSum
3. 动态规划
  * 基于1和2的动态规划题
