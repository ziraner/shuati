Hamming Distance 解题报告

The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.

Given two integers`x`and`y`, calculate the Hamming distance.

**Note:**  
0 ≤`x`,`y`&lt; 231.

**Example:**

```
Input: x = 1, y = 4
Output: 2
Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
The above arrows point to positions where the corresponding bits are different.
```

Idea:

先把x和y取异或，如果不同的话对应的二进制位是1，在判断有多少个1

```
class Solution(object):
    def hammingDistance(self, x, y):
        """
        :type x: int
        :type y: int
        :rtype: int
        """
        cnt = 0
        z = x ^ y
        for i in xrange(32):
            if z & (1 << i) != 0:
                cnt += 1
        return cnt
```



