Best Time to Buy and Sell Stock 解题报告

Say you have an array for which theithelement is the price of a given stock on dayi.

If you were only permitted to complete at most one transaction \(ie, buy one and sell one share of the stock\), design an algorithm to find the maximum profit.

**Example 1:**

```
Input: [7, 1, 5, 3, 6, 4] 
Output: 5
max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```

**Example 2:**

```
Input: [7, 6, 4, 3, 1]
Output: 0
In this case, no transaction is done, i.e. max profit = 0.
```

Idea:

注意ans不能为负的，所以ans的初始值要为0

```
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        from sys import maxint
        ans, minPrice = 0, maxint
        for i in xrange(len(prices)):
            if i != 0:
                ans = max(ans, prices[i] - minPrice)
            minPrice = min(minPrice, prices[i])
        return ans
```



  


