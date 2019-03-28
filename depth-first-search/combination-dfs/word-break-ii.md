Word Break II 解题报告

Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

**Example**

Gieve s =`lintcode`,  
dict =`["de", "ding", "co", "code", "lint"]`.

A solution is`["lint code", "lint co de"]`.

一个最基本的想法就是跟I一样，除了进行DFS。代码如下。但是过不了，时间太长了

```
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: List[str]
        """
        if not s or not wordDict:
            return []
        words = self.getWordDict(wordDict)
        self.maxLength = self.getMaxLength(wordDict)
        ans, sent = [], []
        self.dfs(wordDict, s, 0, ans, sent)
        return ans
    def dfs(self, wordDict, s, pos, ans, sent):
        if pos == len(s):
            ans.append(' '.join(sent))
            return
        for length in xrange(self.maxLength):
            word = s[pos: pos + length + 1]
            if word not in wordDict:
                continue
            sent.append(word)
            self.dfs(wordDict, s, pos + length + 1, ans, sent)
            sent.pop()

    def getWordDict(self, wordDict):
        words = set([])
        for word in wordDict:
            words.add(word)
        return words
    def getMaxLength(self, wordDict):
        length = 0
        for word in wordDict:
            if len(word) > length:
                length = len(word)
        return length
```

考虑到DFS的过程中有重复的情况，比如说  
apple n feng  
app len feng  
如果存在以上2种划分，那么feng这个字符串会被反复计算，在这里至少计算了2次。我们使用一个Hashmap把对应字符串的解记下来，这样就能避免重复的计算。 否则这一道题目会超时。

所以我们的思路就是将所有可以划分为单词的string记录在一个hashmap中， 记录的是所有的可以组成sentence的情况，是一个list。那么我们有下列代码：

```
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: List[str]
        """
        self.ans_set = {}
        self.words = self.convertToDict(wordDict)
        return self.dfs(s)
    def dfs(self, s):
        if s in self.ans_set:
            return self.ans_set[s]
        ans = []
        for i in xrange(len(s)):
            s1 = s[:i + 1]
            s2 = s[i + 1:]
            if s1 in self.words:
                if not s2:
                    ans.append(s1)
                    break
                lst = self.dfs(s2)
                if not lst:
                    continue
                for sentence in lst:
                    new_sentence = s1 + " " + sentence
                    ans.append(new_sentence)
        self.ans_set[s] = ans[:]
        return ans

    def convertToDict(self, wordDict):
        words = set([])
        for word in wordDict:
            words.add(word)
        return words
```



