Lintcode 140: Fast Power 解题报告

Problem:

Calculate the**an % b**where a, b and n are all 32bit integers.

Idea:

跟pow x, n 一样，取模操作可以有结合律，所以把n表示成二进制即可。

Solution:

```
class Solution:
    """
    @param a: A 32bit integer
    @param b: A 32bit integer
    @param n: A 32bit integer
    @return: An integer
    """
    def fastPower(self, a, b, n):
        # write your code here
        ans = 1
        while n > 0:
            if n % 2==1:
                ans = ans * a % b
            a = a * a % b
            n = n / 2
        return ans % b
```



