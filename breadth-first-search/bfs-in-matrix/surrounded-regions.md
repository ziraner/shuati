Surrounded Regions 解题报告

Given a 2D board containing`'X'`and`'O'`, capture all regions surrounded by`'X'`.

A region is captured by flipping all`'O'`'s into`'X'`'s in that surrounded region.

**Example**

```
X X X X
X O O X
X X O X
X O X X

```

After capture all regions surrounded by`'X'`, the board should be:

```
X X X X
X X X X
X X X X
X O X X

```

Idea:

矩阵上面的BFS，只对四条边上的"O"进行BFS，不需要visited矩阵直接在原矩阵上修改因为被BFS过的“O”本来就需要跟没被BFS的"O"区分开

```
class Solution(object):
    def solve(self, board):
        """
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        if not board or not board[0]:
            return
        m, n = len(board), len(board[0])
        for i in xrange(m):
            if board[i][0] == 'O':
                self.bfs(board, i, 0)
            if board[i][n - 1] == 'O':
                self.bfs(board, i, n - 1)
        for j in xrange(n):
            if board[0][j] == 'O':
                self.bfs(board, 0, j)
            if board[m - 1][j] == 'O':
                self.bfs(board, m - 1, j)
        for i in xrange(m):
            for j in xrange(n):
                if board[i][j] == "#":
                    board[i][j] = 'O'
                else:
                    board[i][j] = "X"
    def bfs(self, board, i, j):
        m, n = len(board), len(board[0])
        q = [(i, j)]
        board[i][j] = "#"
        while q:
            x, y = q.pop(0)
            for deltax, deltay in [[1, 0], [-1, 0], [0, -1], [0, 1]]:
                xx, yy = x + deltax, y + deltay
                if xx >= 0 and xx < m and yy >= 0 and yy < n and board[xx][yy] == 'O':
                    board[xx][yy] = "#"
                    q.append((xx, yy))
```



