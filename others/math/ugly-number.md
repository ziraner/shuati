Ugly Number 解题报告

Write a program to check whether a given number is an`ugly`number\`.

`Ugly numbers`are positive numbers whose prime factors only include`2`,`3`,`5`. For example,`6`,`8`are ugly while`14`is not ugly since it includes another prime factor`7`.

##### Notice

Note that`1`is typically treated as an ugly number.

```
class Solution:
    """
    @param: num: An integer
    @return: true if num is an ugly number or false
    """
    def isUgly(self, num):
        # write your code here
        while num >= 2 and num % 2 == 0:
            num /= 2
        while num >= 3 and num % 3 == 0:
            num /= 3
        while num >= 5 and num % 5 == 0:
            num /= 5
        return num == 1
```



