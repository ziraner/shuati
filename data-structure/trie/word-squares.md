Word Squares 解题报告

Given a set of words**without duplicates**, find all[`word squares`](https://en.wikipedia.org/wiki/Word_square)you can build from them.

A sequence of words forms a valid word square if the kth row and column read the exact same string, where 0 ≤ k &lt; max\(numRows, numColumns\).

For example, the word sequence`["ball","area","lead","lady"]`forms a word square because each word reads the same both horizontally and vertically.

```
b a l l
a r e a
l e a d
l a d y
```

##### Notice

* There are at least 1 and at most 1000 words.
* All words will have the exact same length.
* Word length is at least 1 and at most 5.
* Each word contains only lowercase English alphabet `a-z`.

**Example**

```
Given a set ["area","lead","wall","lady","ball"]
return [["wall","area","lead","lady"],["ball","area","lead","lady"]]
Explanation:
The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).

Given a set ["abat","baba","atan","atal"]
return [["baba","abat","baba","atan"],["baba","abat","baba","atal"]]
Explanation:
The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).
```

思路：

这个题目利用Trie树前缀的特性，将所有以这个前缀开头的单词存在前缀节点当中。  
DFS的时候不是基于Trie树的node而是简单的将整个words转换成Trie进行DFS。在DFS中在已有的words中找到我们要的前缀，然后通过这个前缀在Trie里面找到单词，然后循环backtracking找到的单词。需要在主循环中将单词一个一个放入square作为init。

```
class Solution(object):
    def wordSquares(self, words):
        """
        :type words: List[str]
        :rtype: List[List[str]]
        """
        ans = []
        trie = Trie()
        for word in words:
            trie.insert(word)
        for word in words:
            self.dfs([word], ans, trie)
        return ans
    def dfs(self, square, ans, trie):
        n = len(square)
        if n == len(square[-1]):
            ans.append(square[:])
            return
        prefix = ''
        for i in xrange(n):
            prefix += square[i][n]
        for word in trie.search(prefix):
            square.append(word)
            self.dfs(square, ans, trie)
            square.pop()
class Trie:
    def __init__(self, ):
        self.root = TrieNode()
    def insert(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node.words.add(word)
            node = node.children[c]
    def search(self, prefix):
        node = self.root
        for c in prefix:
            if c not in node.children:
                return set([])
            node = node.children[c]
        return node.words
class TrieNode:
    def __init__(self, ):
        self.children = {}
        self.words = set([])
```



