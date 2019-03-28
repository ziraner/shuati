Stone Game 解题报告

There is a stone game.At the beginning of the game the player picks`n`piles of stones in a line.

The goal is to merge the stones in one pile observing the following rules:

1. At each step of the game,the player can merge two adjacent piles to a new pile.
2. The score is the number of stones in the new pile.

You are to determine the minimum of the total score.

**Example**

For`[4, 1, 1, 4]`, in the best solution, the total score is`18`:

```
1. Merge second and third piles => [4, 2, 4], score +2
2. Merge the first two piles => [6, 4]，score +6
3. Merge the last two piles => [10], score +10
```

Other two examples:  
`[1, 1, 1, 1]`return`8`  
`[4, 4, 5, 9]`return`43`

思路：是一道区间类dp的题目

dp\[i\]\[j\] 表示把第i到第j个石子合并到一起的最小花费

预处理sum\[i,j\] 表示i到j所有石子价值和  
dp\[i\]\[j\] = min\(dp\[i\]\[k\]+dp\[k+1\]\[j\]+sum\[i,j\]\) 对于所有k属于{i,j}

```
from sys import maxint
class Solution:
    """
    @param: A: An integer array
    @return: An integer
    """
    def stoneGame(self, A):
        # write your code here
        if not A:
            return 0
        n = len(A)
        self.dp = [[maxint for _ in range(n)] for _ in range(n)]
        self.sum = [[0 for _ in range(n)] for _ in range(n)]
        for i in range(n):
            self.sum[i][i] = A[i]
            for j in range(i + 1, n):
                self.sum[i][j] = self.sum[i][j - 1] + A[j]
        return self.memorysearch(0, n - 1)
    def memorysearch(self, x, y):
        if self.dp[x][y] != maxint:
            return self.dp[x][y]
        if x == y:
            # cannot merget with itself, so value is 0
            self.dp[x][y] = 0
        # i + 1 can == y, so has to loop until y - 1
        for i in range(x, y):
            l = self.memorysearch(x, i)
            r = self.memorysearch(i + 1, y)
            # current merging cost is sum: from left to right
            self.dp[x][y] = min(l + r + self.sum[x][y], self.dp[x][y])
        return self.dp[x][y]
```



