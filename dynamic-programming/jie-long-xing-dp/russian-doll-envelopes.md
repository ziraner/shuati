Russian Doll Envelopes 解题报告

You have a number of envelopes with widths and heights given as a pair of integers`(w, h)`. One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

What is the maximum number of envelopes can you Russian doll? \(put one inside other\)

**Example**

Given envelopes =`[[5,4],[6,4],[6,7],[2,3]]`,  
the maximum number of envelopes you can Russian doll is 3 \(\[2,3\] =&gt; \[5,4\] =&gt; \[6,7\]\).

思路，转自：[http://blog.csdn.net/magicbean2/article/details/77140422](http://blog.csdn.net/magicbean2/article/details/77140422)

只要巧妙地变换一下，就是一道最长递增子序列的题目。我们用题目中给出的例子进行分析。如果在x维度上升序排列，而在x相同的情况下，在y维度上降序排列，那么上例的排序结果就是：\[\[2,3\], \[5,4\], \[6,7\], \[6,4\]\]。我们发现，只要在y维度上找到最长递增子序列，就对应了本题的答案。为什么呢？因为如果在y维度上如果已经递增了，那么在x维度上必然是递增的，用反证法来证明：对于有序区间\[s1,e1\]和\[s2,e2\]（意味着s1 &lt;= s2），如果e1 &lt; e2，假设s1 == s2，那么区间\[s2,e2\]必然在排序的时候会排在\[s1,e1\]之前，与有序前区间这一前提矛盾。所以必然s1 &lt; s2。

从理论上证明正确性之后，我们考虑最长子序列问题的两个经典解法：1）动态规划；2）二分查找。前者的时间复杂度是O\(n^2\)，后者的时间复杂度是O\(nlogn\)。我们这里实现的是二分查找。

```
class Solution(object):
    def maxEnvelopes(self, envelopes):
        """
        :type envelopes: List[List[int]]
        :rtype: int
        """
        if not envelopes or not envelopes[0]:
            return 0
        envelopes.sort(key = lambda x : (x[0] , -x[1]))
        from sys import maxint
        n = len(envelopes)
        f = [maxint for _ in xrange(n)]
        for i in xrange(n):
            idx = self.binarySearch(f, envelopes[i][1])
            f[idx] = envelopes[i][1]
        i = n - 1
        while True:
            if f[i] != maxint:
                break
            i -= 1
        return i + 1
    def binarySearch(self, f, val):
        start, end = 0, len(f) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if f[mid] < val:
                start = mid
            else:
                end = mid
        if f[start] >= val:
            return start
        return end
```



