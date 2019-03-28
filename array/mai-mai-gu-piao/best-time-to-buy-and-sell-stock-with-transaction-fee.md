Best Time to Buy and Sell Stock with Transaction Fee 解题报告

Your are given an array of integers`prices`, for which the`i`-th element is the price of a given stock on day`i`; and a non-negative integer`fee`representing a transaction fee.

You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction. You may not buy more than 1 share of a stock at a time \(ie. you must sell the stock share before you buy again.\)

Return the maximum profit you can make.

**Example 1:**

```
Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
Buying at prices[0] = 1
Selling at prices[3] = 8
Buying at prices[4] = 4
Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

Idea:

这个题沿用Best Time to Buy and Sell Stock with Cooldown的思路，设buy和sell两个array

`buy[i] = max{buy[i-1], sell[i-1] - prices[i]}`

`sell[i] = max{sell[i - 1], buy[i-1] + prices[i] - fee}`

```
class Solution(object):
    def maxProfit(self, prices, fee):
        """
        :type prices: List[int]
        :type fee: int
        :rtype: int
        """
        if not prices:
            return 0
        n = len(prices)
        buy = [0 for _ in xrange(n)]
        sell = [0 for _ in xrange(n)]
        buy[0] = -prices[0]
        for i in xrange(1, n):
            buy[i] = max(buy[i - 1], sell[i - 1] - prices[i])
            sell[i] = max(sell[i - 1], buy[i - 1] + prices[i] - fee)
        return max(sell[n - 1], 0)
```



