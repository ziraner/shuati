Best Time to Buy and Sell Stock IV 解题报告

Say you have an array for which theithelement is the price of a given stock on dayi.

Design an algorithm to find the maximum profit. You may complete at most**k**transactions.

**Note:**  
You may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

Idea:

动态规划。传统的动态规划即第i天进行j次transaction的最大利润为f，有一个问题在于，第i - 1天进行了卖操作，其实可以和第i天进行一次买操作合并为一次操作，如果只定义一个数组，那么会多count一次这种情况的transaction。

所以一个数组不够，需要两个数组。

global\[i\]\[j\]为全局变量，即全局的第i天进行j次交易的最大利润

local\[i\]\[j\]为局部变量，即第i天必须进行交易所产生的local最大利润

```
local[i][j] = max(global[i-1][j-1] + max(diff,0), local[i-1][j]+diff)
global[i][j] = max(local[i][j], global[i-1][j])
```

第二个式子很好理解，全局的是当前天局部j次交易和前一天的全局j次交易之间的最大值

第一个式子是，局部的第i天进行j次交易 = 全局的i-1天j -1次交易+最后一天的一次交易（如果挣钱的话）和局部的i-1天j次交易加上最后一天一定做得交易（不论赚钱与否）这样就不会丢掉上述所说的情况了

这个题目需要在动态规划之前判断k和n的关系如果k&gt;=n的话那么退化为Best Time to Buy and Sell Stock II

这个题目python写的话需要注意global是python reserve的关键词，需要用别的词儿

```
class Solution(object):
    def maxProfit(self, k, prices):
        """
        :type k: int
        :type prices: List[int]
        :rtype: int
        """
        n = len(prices)
        if k >= n:
            return self.maxProfit2(prices)
        globl = [[0 for _ in xrange(k + 1)] for _ in xrange(n)]
        local = [[0 for _ in xrange(k + 1)] for _ in xrange(n)]
        for i in xrange(1, n):
            diff = prices[i] - prices[i - 1]
            for j in xrange(1, k + 1):
                local[i][j] = max(globl[i - 1][j - 1] + max(diff, 0), local[i - 1][j] + diff)
                globl[i][j] = max(local[i][j], globl[i - 1][j])
        return globl[n - 1][k]
    def maxProfit2(self, prices):
        ans = 0
        for i in xrange(1, len(prices)):
            diff = prices[i] - prices[i - 1]
            if diff > 0:
                ans += diff
        return ans
```



