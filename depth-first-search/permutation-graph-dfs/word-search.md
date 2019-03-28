Word Search 解题报告

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

Given board =

```
[
  "ABCE",
  "SFCS",
  "ADEE"
]
```

word = `"ABCCED"`, -&gt; returns `true`,  
word = `"SEE"`, -&gt; returns `true`,  
word = `"ABCB"`, -&gt; returns `false`.

Idea:

在二维矩阵上面的DFS题目 朗读并背诵全文

```
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        if not word:
            return True
        if not board or not board[0]:
            return False
        m, n = len(board), len(board[0])
        visited = [[False for _ in xrange(n)] for _ in xrange(m)]
        for i in xrange(m):
            for j in xrange(n):
                if self.dfs(board, word, visited, i, j, 0):
                    return True
        return False
    def dfs(self, board, word, visited, i, j, pos):
        if pos == len(word):
            return True
        delta = [[0, 1], [0, -1], [1, 0], [-1, 0]]
        m, n = len(board), len(board[0])
        if i < 0 or i >= m or j < 0 or j >= n:
            return False
        if visited[i][j] or board[i][j] != word[pos]:
            return False
        visited[i][j] = True
        for deltai, deltaj in delta:
            ii, jj = i + deltai, j + deltaj
            if self.dfs(board, word, visited, ii, jj, pos + 1):
                return True
        visited[i][j] = False
        return False
```



