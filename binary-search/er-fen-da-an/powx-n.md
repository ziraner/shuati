Lintcode 428: Pow\(x, n\) 解题报告

Problem:

Implement pow\(x, n\).

##### Notice

You don't need to care about the precision of your answer, it's acceptable if the expected answer and your answer 's difference is smaller than`1e-3`.

**Example**

```
Pow(2.1, 3) = 9.261
Pow(0, 1) = 0
Pow(1, 0) = 1
```

Idea:

将n表示成2进制，则答案就是x的2的不为零次方相乘，总共相乘的次数为logn，所以就是logn的复杂度。

Solution:

```
class Solution:
    """
    @param: x: the base number
    @param: n: the power number
    @return: the result
    """
    def myPow(self, x, n):
        # write your code here
        if n < 0:
            x = 1.0 / x
            n = -n
        # O(n): guo bu liao
        """
        ans = 1.0
        for i in xrange(0, n):
            ans = ans * x
        return ans
        """
        ans, factor = 1.0, x * 1.0
        while n != 0:
            if n % 2 == 1:
                ans *= factor
            n = n / 2
            factor *= factor
        return ans


```



