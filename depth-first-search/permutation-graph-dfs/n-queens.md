N-Queen解题报告

The n-queens puzzle is the problem of placing n queens on an`n×n`chessboard such that no two queens attack each other.

Given an integer`n`, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where`'Q'`and`'.'`both indicate a queen and an empty space respectively.  
**Example**

There exist two distinct solutions to the 4-queens puzzle:

```
[
  // Solution 1
  [".Q..",
   "...Q",
   "Q...",
   "..Q."
  ],
  // Solution 2
  ["..Q.",
   "Q...",
   "...Q",
   ".Q.."
  ]
]
```

思路：

先用dfs递归每一行的皇后都放在哪个位置，保存进一个sol函数，然后当sol函数满足题意的时候，加进ans的时候顺便build了棋盘

isValid函数怎么写：  
因为solution中保存的是当前行，queen所在的列数，所以判断是否是一行自动判断完了，就剩了，1.判断是否跟前面皇后有一个列上的2.是否跟前面皇后有45度对角线上的 x1 - y1 = x2 - y2 3.是否跟前面皇后有-45度对角线上的 x2 + y2 = x1 + y1

```
class Solution:
    """
    @param: n: The number of queens
    @return: All distinct solutions
    """
    def solveNQueens(self, n):
        # write your code here
        ans, sol = [], []
        self.dfs(sol, ans, n)
        return ans
    def dfs(self, sol, ans, n):
        if len(sol) == n:
            ans.append(self.buildAnswer(sol))
            return
        for j in xrange(n):
            if self.isValid(sol, j):
                sol.append(j)
                self.dfs(sol, ans, n)
                sol.pop()
    def buildAnswer(self, sol):
        n = len(sol)
        board = []
        for i in xrange(n):
            row = ['.' for _ in xrange(n)]
            row[sol[i]] = 'Q'
            board.append(''.join(row)[:])
        return board
    def isValid(self, sol, j):
        j_row = len(sol)
        for i_row, i in enumerate(sol):
            if i == j:
                return False
            if j_row + j == i_row + i:
                return False
            if j_row - j == i_row - i:
                return False
        return True
```



