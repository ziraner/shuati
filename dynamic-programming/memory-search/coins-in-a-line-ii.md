Coins in a Line II解题报告

There are n coins with different value in a line. Two players take turns to take one or two coins from left side until there are no more coins left. The player who take the coins with the most value wins.

Could you please decide the**first**player will win or lose?

**Example**

Given values array A =`[1,2,2]`, return`true`.

Given A =`[1,2,4]`, return`false`.

同Coins in a Line一样是一个博弈类DP，用memorizationsearch来做

dp\[i\] 现在还剩i个硬币，现在先手取硬币的人最后最多取硬币价值  
dp\[i\] = max\(min\(dp\[i-2\], dp\[i-3\]\)+coin\[n-i\] \) ， \(min\(dp\[i-3\],dp\[i-4\]\)+coin\[n-i\]+coin\[n-i+1\] \) 这个方程的理解跟一一样，你先手里面有选1跟选2两种情况，不论哪种情况，后手都会有自己的判断选择大的那种，所以剩下的肯定是最小的那种。

```
class Solution:
    """
    @param: values: a vector of integers
    @return: a boolean which equals to true if the first player will win
    """
    def firstWillWin(self, values):
        # write your code here
        if not values:
            return False
        n = len(values)
        dp = [-1 for _ in range(n + 1)]
        return self.memorysearch(n, values, dp) > sum(values) / 2
    def memorysearch(self, i, values, dp):
        n = len(values)
        if dp[i] != -1:
            return dp[i]
        if i == 0:
            dp[i] = 0
        elif i == 1:
            dp[i] = values[n - 1]
        elif i == 2:
            dp[i] = values[n - 1] + values[n - 2]
        elif i == 3:
            dp[i] = values[n - 2] + values[n - 3]
        else:
            v1 = values[n - i] + min(self.memorysearch(i - 2, values, dp), \
                    self.memorysearch(i - 3, values, dp))
            v2 = values[n - i + 1] + values[n - i] + \
                    min(self.memorysearch(i - 3, values, dp), self.memorysearch(i - 4, values, dp))
            dp[i] = max(v1, v2)
        return dp[i]
```

  


