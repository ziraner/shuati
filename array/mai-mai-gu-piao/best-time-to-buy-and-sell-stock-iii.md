Best Time to Buy and Sell Stock III 解题报告

Say you have an array for which the_i\_thelement is the price of a given stock on day\_i_.

Design an algorithm to find the**maximum**profit. You may complete at most\_two\_transactions.

##### Notice

You may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

跟maximum subarray II 类似，维护两个数组，从左向右最大的profit和从右向左最大的profit，最后总的就是max（左+右，当前）

```
from sys import maxint
class Solution:
    """
    @param: prices: Given an integer array
    @return: Maximum profit
    """
    def maxProfit(self, prices):
        # write your code here
        n = len(prices)
        if n < 2:
            return 0
        left = [0 for _ in xrange(n)]
        right = [0 for _ in xrange(n)]
        minPrice = maxint
        for i in xrange(n):
            if i != 0:
                left[i] = max(left[i - 1], prices[i] - minPrice)
            minPrice = min(minPrice, prices[i])
        maxPrice = -maxint
        for i in xrange(n - 1, -1, -1):
            if i != n - 1:
                right[i] = max(right[i + 1], maxPrice - prices[i])
            maxPrice = max(maxPrice, prices[i])
        ans = 0
        for i in xrange(n):
            ans = max(ans, left[i] + right[i])
        return ans
```



