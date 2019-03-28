Ugly Number II 解题报告

Ugly number is a number that only have factors`2`,`3`and`5`.

Design an algorithm to find the\_n\_th ugly number. The first 10 ugly numbers are`1, 2, 3, 4, 5, 6, 8, 9, 10, 12...`

##### Notice

Note that`1`is typically treated as an ugly number.

**Example**

If`n=9`, return`10`.

方法一：

heapq，需要建一个set，确保不重复计算，O\(nlogn\)时间复杂度

```
class Solution:
    """
    @param: n: An integer
    @return: the nth prime number as description.
    """
    def nthUglyNumber(self, n):
        # write your code here
        # O(nlogn) heap
        """
        from heapq import heappush, heappop
        h = [1]
        s = set([1])
        cnt = 1
        while True:
            val = heappop(h)
            if cnt == n:
                return val
            for prime in [2, 3, 5]:
                num = prime * val
                if num in s:
                    continue
                heappush(h, num)
                s.add(num)
            cnt += 1
```

方法二：

对同一个list可以分解为3 lists，维护三个idx指针和三个值  
l2: 1\*2, 2\*2, 3\*2, 4\*2, 5\*2, ... 指针idx2  
l3: 1\*3, 2\*3, 3\*3, 4\*3, 5\*3, ... 指针idx3  
l5: 1\*5, 2\*5, 3\*5, 4\*5, 5\*5, ... 指针idx5  
每次从这几个指针对应的三个数中取出min，然后判断这个数是否等于当前lst到的数，如果相等则++指针可以避免重复。

```
class Solution:
    """
    @param: n: An integer
    @return: the nth prime number as description.
    """
    def nthUglyNumber(self, n):
        # write your code here
        # O(n)
        ugly = [1]
        i2, i3, i5 = 0, 0, 0
        while len(ugly) < n:
            m2, m3, m5 = ugly[i2] * 2, ugly[i3] * 3, ugly[i5] * 5
            m = min(m2, m3, m5)
            if m == m2:
                i2 += 1
            if m == m3:
                i3 += 1
            if m == m5:
                i5 += 1
            ugly.append(m)
        return ugly[-1]
```



