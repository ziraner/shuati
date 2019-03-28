Word Ladder II 解题报告

Given two words \(startandend\), and a dictionary, find all shortest transformation sequence\(s\) fromstarttoend, such that:

1. Only one letter can be changed at a time
2. Each intermediate word must exist in the dictionary

##### Notice

* All words have the same length.
* All words contain only lowercase alphabetic characters.

思路：

先从end到start做BFS算出来每个单词到end的最小距离，保存在一个hashmap中，不妨叫dist。这里BFS不需要按层来进行，也不需要visited因为dist是一个hashmap

然后从start带着dist做DFS，每次向level -1的单词递归，如果遇到了end则加进ans中。递归的返回条件是lst中最后一个单词是end

```
class Solution(object):
    def findLadders(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: List[List[str]]
        """
        if endWord not in wordList:
            return []
        wordDict = self.addToDict(wordList, beginWord)
        dist = self.bfs(wordDict, beginWord, endWord)
        ans, lst = [], [beginWord]
        self.dfs(wordDict, dist, endWord, ans, lst)
        return ans
    def bfs(self, wordDict, beginWord, endWord):
        dist = {endWord: 0}
        q = [endWord]
        while q:
            tmp = q.pop(0)
            if tmp == beginWord:
                return dist
            for word in self.getNextWords(tmp, wordDict):
                if word in dist:
                    continue
                q.append(word)
                dist[word] = dist[tmp] + 1
        return dist
    def dfs(self, wordDict, dist, endWord, ans, lst):
        curtword = lst[-1]
        if curtword == endWord:
            ans.append(lst[:])
            return
        for nextword in self.getNextWords(curtword, wordDict):
            if nextword not in dist:
                continue
            if dist[curtword] - 1 != dist[nextword]:
                continue
            lst.append(nextword)
            self.dfs(wordDict, dist, endWord, ans, lst)
            lst.pop()
    def getNextWords(self, word, wordDict):
        alphabet = "abcdefghijklmnopqrstuvwxyz"
        next_words = []
        for i in xrange(len(word)):
            for c in alphabet:
                new_word = word[:i] + c + word[i + 1:]
                if new_word == word:
                    continue
                if new_word not in wordDict:
                    continue
                next_words.append(new_word)
        return next_words
    def addToDict(self, wordList, beginWord):
        wordDict = set([])
        for word in wordList:
            wordDict.add(word)
        wordDict.add(beginWord)
        return wordDict
```



