Word Ladder解题报告

Given two words \(beginWord and endWord\), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

For example,

Given: beginWord=`"hit"`endWord=`"cog"`wordList=`["hot","dot","dog","lot","log","cog"]`

As one shortest transformation is`"hit" -> "hot" -> "dot" -> "dog" -> "cog"`,return its length`5`.

**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume beginWord and endWord are non-empty and are not the same.

**UPDATE \(2017/1/20\):**  
ThewordListparameter had been changed to a list of strings \(instead of a set of strings\). Please reload the code definition to get the latest changes.

Idea:

图中的层级BFS，因为要求层数。数据结构需要一个q和一个visited hash

Update中不给字典了就需要自己建立字典，可以把visited和字典合并为一个set

```
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: int
        """
        wordDict = self.getDict(beginWord, wordList)
        q = [beginWord]
        wordDict.remove(beginWord)
        ans = 1
        while q:
            size = len(q)
            for i in xrange(size):
                tmp = q.pop(0)
                if tmp == endWord:
                    return ans
                for word in self.getNextWords(tmp, wordDict):
                    q.append(word)
                    wordDict.remove(word)
            ans += 1
        return 0

    def getDict(self, beginWord, wordList):
        wordDict = set([])
        wordDict.add(beginWord)
        for word in wordList:
            wordDict.add(word)
        return wordDict
    def getNextWords(self, word, wordDict):
        ans = []
        ALPHABET = 'abcdefghijklmnopqrstuvwxyz'
        for i in xrange(len(word)):
            for c in ALPHABET:
                tmp = word[:i] + c + word[i + 1:]
                if tmp not in wordDict:
                    continue
                ans.append(tmp[:])
        return ans
```



