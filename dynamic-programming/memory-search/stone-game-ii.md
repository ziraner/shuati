Stone Game II解题报告

There is a stone game.At the beginning of the game the player picks n piles of stones`in a circle`.

The goal is to merge the stones in one pile observing the following rules:

At each step of the game,the player can merge two adjacent piles to a new pile.  
The score is the number of stones in the new pile.  
You are to determine the minimum of the total score.  
**Example**

For`[4, 1, 1, 4]`, in the best solution, the total score is`18`:

```
1. Merge second and third piles =
>
 [4, 2, 4], score +2
2. Merge the first two piles =
>
 [6, 4]，score +6
3. Merge the last two piles =
>
 [10], score +10

```

Other two examples:  
`[1, 1, 1, 1]`return`8`  
`[4, 4, 5, 9]`return`43`

  
把原数组扩展成两倍，然后每个位置做一个window为n的stone game I

```
from sys import maxint
class Solution:
    """
    @param: A: An integer array
    @return: An integer
    """
    def stoneGame2(self, A):
        # write your code here
        if not A:
            return 0
        n = len(A)
        self.dp = [[maxint for _ in range(2 * n)] for _ in range(2 * n)]
        self.flag = [[False for _ in range(2 * n)] for _ in range(2 * n)]
        self.sum = [[0 for _ in range(2 * n)] for _ in range(2 * n)]
        for i in range(2 * n):
            self.sum[i][i] = A[i % n]
            for j in range(i + 1, 2 * n):
                self.sum[i][j] = self.sum[i][j - 1] + A[j % n]
        ans = maxint
        for i in range(n):
            ans = min(ans, self.memorysearch(i, i + n - 1))
        return ans
    def memorysearch(self, i, j):
        if self.flag[i][j]:
            return self.dp[i][j]
        self.flag[i][j] = True
        if i == j:
            self.dp[i][j] = 0
        for k in range(i, j):
            l = self.memorysearch(i, k)
            r = self.memorysearch(k + 1, j)
            self.dp[i][j] = min(self.dp[i][j], l + r + self.sum[i][j])
        return self.dp[i][j]
            
```



