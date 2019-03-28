Best Time to Buy and Sell Stock II

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like \(ie, buy one and sell one share of the stock multiple times\). However, you may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

**Example**

Given an example\[2,1,2,0,1\], return 2

Idea:

贪心法，比较相邻两个的diff，大于零就加入ans

```
class Solution:
    """
    @param: prices: Given an integer array
    @return: Maximum profit
    """
    def maxProfit(self, prices):
        # write your code here
        ans = 0
        for i in xrange(1, len(prices)):
            diff = prices[i] - prices[i - 1]
            if diff > 0:
                ans += diff
        return ans
```



