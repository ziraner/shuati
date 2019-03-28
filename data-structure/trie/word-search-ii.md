Word Search II 解题报告

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

For example,  
Given **words**=`["oath","pea","eat","rain"]`and **board**=

```
[ ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
```

Return

`["eat","oath"]`

**Note:**  
You may assume that all inputs are consist of lowercase letters`a-z`.

思路：

如果用hash的话需要一个一个单词看过去，很浪费时间。

所以要用Trie优化，看前缀是否存在，不存在的话直接剪枝，不需要往下进行了，比hash优化很多；且不需要以单词为单位，直接以Tire树的node为基点进行DFS既可。因为如果有两个单词leet, leetcode,那么其实一次向下搜索可以找到这两个。这个题目因为已经不带着word进行DFS了，所以要将word存在Trie树里面，即再建一个TrieNode变量存储当前节点如果是word的话是个什么word。

总结：这个题目考察的是TrieTree的DFS问题，即带着node进行DFS，这个DFS也需要有word search I的DFS的基础

```
class Solution(object):
    def findWords(self, board, words):
        """
        :type board: List[List[str]]
        :type words: List[str]
        :rtype: List[str]
        """
        if not board or not board[0]:
            return None
        m, n = len(board), len(board[0])
        trie = Trie()
        visited = [[False for _ in xrange(n)] for _ in xrange(m)]
        ans = []
        for word in words:
            trie.insert(word)
        for i in xrange(m):
            for j in xrange(n):
                self.dfs(board, trie.root, visited, i, j, ans)
        return ans
    def dfs(self, board, node, visited, i, j, ans):
        if node.isWord:
            if node.word not in ans:
                ans.append(node.word)
        m, n = len(board), len(board[0])
        if i < 0 or i >= m or j < 0 or j >= n or visited[i][j] or board[i][j] not in node.children:
            return
        visited[i][j] = True
        for deltax, deltay in [[0, -1], [0, 1], [-1, 0], [1, 0]]:
            ii, jj = i + deltax, j + deltay
            self.dfs(board, node.children[board[i][j]], visited, ii, jj, ans)
        visited[i][j] = False
class TrieNode:
    def __init__(self, ):
        self.children = {}
        self.isWord = False
        self.word = ''
class Trie:
    def __init__(self, ):
        self.root = TrieNode()
    def insert(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.isWord = True
        node.word = word
```



