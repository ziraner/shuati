Coins in a Line 解题报告

There are n coins in a line. Two players take turns to take one or two coins from right side until there are no more coins left. The player who take the last coin wins.

Could you please decide the**first**play will win or lose?

**Example**

n =`1`, return`true`.

n =`2`, return`true`.

n =`3`, return`false`.

n =`4`, return`true`.

n =`5`, return`true`.

博弈类DP，从大到小研究状态

dp\[i\] 现在还剩i个硬币，现在先手取硬币的人最后输赢状况  
dp\[i\] = \(dp\[i-2\]&& dp\[i-3\]\) \|\| \(dp\[i-3\]&& dp\[i-4\] \) 这个方程的意思是说，选择一个方式拿一个或者拿两个，不论后手拿一个或者拿两个你都要赢。

写方程的时候可以通过dp代替flag数组，刚开始dp保存-1，如果能赢1，不能赢0，-1代表没遍历过。

```
class Solution:
    """
    @param: n: An integer
    @return: A boolean which equals to true if the first player will win
    """
    def firstWillWin(self, n):
        # write your code here
        # function
        dp = [-1 for _ in range(n + 1)]
        return self.memorysearch(n, dp)
        # memorysearch
    def memorysearch(self, n, dp):
        if dp[n] != -1:
            return dp[n] == 1
        if n <= 0:
            dp[n] = 0
        elif n <= 2:
            dp[n] = 1
        elif n == 3:
            dp[n] = 0
        else:
            if self.memorysearch(n - 3, dp) and self.memorysearch(n - 2, dp) or \
                    self.memorysearch(n - 3, dp) and self.memorysearch(n - 4, dp):
                dp[n] = 1
            else:
                dp[n] = 0
        return dp[n] == 1
```



