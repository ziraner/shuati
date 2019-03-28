H-Index 解题报告

Given an array of citations \(each citation is a non-negative integer\) of a researcher, write a function to compute the researcher's h-index.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): "A scientist has index h if h of his/her N papers have **at least  **h citations each, and the otherN − h papers have **no more than  **h citations each."

For example, given`citations = [3, 0, 6, 1, 5]`, which means the researcher has`5`papers in total and each of them had received`3, 0, 6, 1, 5`citations respectively. Since the researcher has`3`papers with **at least**`3`citations each and the remaining two with **no more than**`3`citations each, his h-index is`3`.

**Note**: If there are several possible values for`h`, the maximum one is taken as the h-index.

Idea: 两种思路。

思路一：从大到小排序，然后从第一个数开始扫。i &gt;= citation\[i\]的话return。最后Corner case return citation的长度

```
class Solution(object):
    def hIndex(self, citations):
        """
        :type citations: List[int]
        :rtype: int
        """        
        citations.sort(key = lambda x: -x)
        for i, c in enumerate(citations):
            if i >= c:
                return i
        return len(citations)
```

思路二：O\(n\)的时间复杂度。建一个O\(n + 1\)的cnt数组统计citation被引用的次数，从0到n，如果大于n则加到n中。

最后从大到小扫一遍cnt数组，如果total的数目大于当前index则index即为所求：至少有h篇论文的引用大于等于h

```
class Solution(object):
    def hIndex(self, citations):
        """
        :type citations: List[int]
        :rtype: int
        """
        n = len(citations)
        cnt = [0 for _ in xrange(n + 1)]
        for c in citations:
            if c >= n:
                cnt[n] += 1
            else:
                cnt[c] += 1
        total = 0
        for h in xrange(n, -1, -1):
            if cnt[h] + total >= h:
                return h
            total += cnt[h]
        return 0
```



