Super Ugly Number 解题报告

Write a program to find the nth super ugly number.

Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size`k`. For example,`[1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32]`is the sequence of the first 12 super ugly numbers given primes =`[2, 7, 13, 19]`of size`4`.

##### Notice

* `1`is a super ugly number for any given primes.
* The given numbers in primes are in ascending order.
* 0 &lt; k ≤ 100, 0 &lt; n ≤ 10^6, 0 &lt; primes\[i\] &lt; 1000

Idea

这个题目是ugly number II的特殊情况，ugly number II只有2,3,5现在有个list。效仿ugly number II

```
class Solution(object):
    def nthSuperUglyNumber(self, n, primes):
        """
        :type n: int
        :type primes: List[int]
        :rtype: int
        """
        ugly = [1]
        m = len(primes)
        idx = [0 for _ in xrange(m)]
        vals = [0 for _ in xrange(m)]
        while len(ugly) != n:
            for i in xrange(m):
                vals[i] = primes[i] * ugly[idx[i]]
            val = min(vals)
            for i in xrange(m):
                if val == vals[i]:
                    idx[i] += 1
            ugly.append(val)
        return ugly[-1]
```



