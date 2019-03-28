Coins in a Line III解题报告

There are\_n\_coins in a line. Two players take turns to take a coin from one of the ends of the line until there are no more coins left. The player with the larger amount of money wins.

Could you please decide the first player will win or lose?

**Example**

Given array A =`[3,2,2]`, return`true`.

Given array A =`[1,2,4]`, return`true`.

Given array A =`[1,20,4]`, return`false`.

这个题牛逼了，是一道，区间+博弈类DP问题。用memorizationsearch来解。

left = min\(dp\[i+2\]\[j\], dp\[i+1\]\[j-1\]\)+coin\[i\] \[i+1,j\]

right = min\(dp\[i\]\[j-2\], dp\[i+1\]\[j-1\]\)+coin\[j\] \[i,j-1\]

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
        self.dp = [[-1 for _ in range(n)] for _ in range(n)]
        return self.memorysearch(0, n - 1, values) > sum(values) / 2
    def memorysearch(self, i, j, values):
        if self.dp[i][j] != -1:
            return self.dp[i][j]
        if i == j:
            self.dp[i][j] = values[i]
        elif i + 1 == j:
            self.dp[i][j] = max(values[i], values[j])
        else:
            l = min(self.memorysearch(i + 2, j, values), self.memorysearch(i + 1, j - 1, values)) + values[i]
            r = min(self.memorysearch(i, j - 2, values), self.memorysearch(i + 1, j - 1, values)) + values[j]
            self.dp[i][j] = max(l, r)
        return self.dp[i][j]
```



