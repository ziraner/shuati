Best Time to Buy and Sell Stock with Cooldown 解题报告

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like \(ie, buy one and sell one share of the stock multiple times\) with the following restrictions:

* You may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).
* After you sell your stock, you cannot buy stock on next day. \(ie, cooldown 1 day\)

**Example:**

```
prices = [1, 2, 3, 0, 2]
maxProfit = 3
transactions = [buy, sell, cooldown, buy, sell]
```

Idea:

转自算法珠玑

对于每一天，有三种动作，buy, sell, cooldown, sell 和 cooldown 可以合并成一种状态，因为手里最终没有股票。最终需要的结果是 sell，即手里股票卖了获得最大利润。我们可以用两个数组来记录当前持股和未持股的状态，令`sell[i]`表示第i天未持股时，获得的最大利润，`buy[i]`表示第i天持有股票时，获得的最大利润。

对于`sell[i]`，最大利润有两种可能，一是今天没动作跟昨天未持股状态一样，二是今天卖了股票，所以状态转移方程如下：

`sell[i] = max{sell[i - 1], buy[i-1] + prices[i]}`

对于`buy[i]`，最大利润有两种可能，一是今天没动作跟昨天持股状态一样，二是前天卖了股票，今天买了股票，因为 cooldown 只能隔天交易，所以今天买股票要追溯到前天的状态。状态转移方程如下：

`buy[i] = max{buy[i-1], sell[i-2] - prices[i]}`

最终我们要求的结果是`sell[n - 1]`，表示最后一天结束时，手里没有股票时的最大利润。

这个算法的空间复杂度是`O(n)`，不过由于`sell[i]`仅仅依赖前一项，`buy[i]`仅仅依赖前两项，所以可以优化到`O(1)`

```
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if not prices:
            return 0
        n = len(prices)
        buy = [0 for _ in xrange(n)]
        sell = [0 for _ in xrange(n)]
        buy[0] = -prices[0]
        for i in xrange(1, n):
            if i >= 2:
                buy[i] = max(buy[i - 1], sell[i - 2] - prices[i])
            else:
                buy[i] = max(buy[i - 1], -prices[i])
            sell[i] = max(sell[i - 1], buy[i - 1] + prices[i])
        return sell[n - 1]
```



