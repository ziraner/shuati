H-Index II 解题报告

What if the`citations`array is sorted in ascending order? Could you optimize your algorithm?

idea:

解法一：H-index的特殊情况，已经排好序了

```
class Solution(object):
    def hIndex(self, citations):
        """
        :type citations: List[int]
        :rtype: int
        """
        n = len(citations)
        for i, c in enumerate(reversed(citations)):
            if i >= c:
                return i
        return len(citations)
```

解法二：二分法

怎么判断什么情况该怎么移？如果citations\[mid\] &gt;= n - mid则说明n - mid可以作为一个valid的h index因为有n - mid个文章的引用大于n - mid，那么它不一定是最大的h index所以要往左边去找更大的即更小的mid；反之就start = mid

最后先判断start，如果满足返回不满足返回end

```
class Solution(object):
    def hIndex(self, citations):
        """
        :type citations: List[int]
        :rtype: int
        """
        if not citations:
            return 0
        n = len(citations)
        start, end = 0, n
        while start + 1 < end:
            mid = (start + end) / 2
            if citations[mid] < n - mid:
                start = mid
            else:
                end = mid
        if citations[start] >= n - start:
            return n - start
        return n - end
```



