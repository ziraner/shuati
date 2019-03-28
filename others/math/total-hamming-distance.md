Total Hamming Distance 解题报告

The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.

Now your job is to find the total Hamming distance between all pairs of the given numbers.

**Example:**

```
Input: 4, 14, 2

Output: 6

Explanation: In binary representation, the 4 is 0100, 14 is 1110, and 2 is 0010 (just
showing the four bits relevant in this case). So the answer will be:
HammingDistance(4, 14) + HammingDistance(4, 2) + HammingDistance(14, 2) = 2 + 2 + 2 = 6.
```

**Note:**

1. Elements of the given array are in the range of`0`to`10^9`
2. Length of the array will not exceed `10^4`.

Idea:

对给出的数组假设里面有n个数，那么统计每个数的二进制表示32位的每一位1的个数，假设为k个，那么0的个数就是n - k个，则对于该位hamming distance就是k \* \(n - k\)

时间复杂度O\(32 \* n\)

```
class Solution(object):
    def totalHammingDistance(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        ans = 0
        for i in xrange(32):
            cnt = 0
            for j in xrange(n):
                if nums[j] & (1 << i) != 0:
                    cnt += 1
            ans += cnt * (n - cnt)
        return ans
```



