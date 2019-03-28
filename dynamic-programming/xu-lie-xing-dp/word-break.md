Word Break(Lintcode && Leetcode) 解题报告

Lintcode:
Given a string s and a dictionary of words dict, determine if s can be break into a space-separated sequence of one or more dictionary words.
**Example**
Gieve s =`lintcode`,  
dict =`["de", "ding", "co", "code", "lint"]`.
A solution is`["lint code", "lint co de"]`.

Idea:
接龙型DP
f\[i\]表示从前面任意一点到i是否可以组成word
注意可以在increasing length的时候stop at dictionary中最长的长度。

```
class Solution(object):
    def wordBreak(self, s, wordDict):
        n = len(s)
        f = [False for _ in xrange(n + 1)]
        f[0] = True
        maxLength = self.getMaxLength(wordDict)
        wordDict = self.convertToDict(wordDict)
        for i in xrange(1, n + 1):
            length = 0
            while i - length >= 0 and length <= maxLength:
                word = s[i - length:i]
                if word in wordDict and f[i - length]:
                    f[i] = True
                    break
                length += 1
        return f[n]
    def convertToDict(self, wordDict):
        hs = set([])
        for word in wordDict:
            hs.add(word)
        return hs
    def getMaxLength(self, wordDict):
        ans = 0
        for word in wordDict:
            ans = max(ans, len(word))
        return ans
```


Leetcode:

Given a **non-empty **stringsand a dictionary wordDict containing a list of **non-empty **words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

For example, given s=`"leetcode"`, dict=`["leet", "code"]`.

Return true because`"leetcode"`can be segmented as`"leet code"`.

**UPDATE \(2017/1/4\):**  
The wordDict parameter had been changed to a list of strings \(instead of a set of strings\). Please reload the code definition to get the latest changes.

Idea:

对于update的话我们新建一个set把wordDict单词存进去就ＯＫ了

对于原题目的一个优化是统计wordDict中最长单词的长度时间复杂度O\(N\*MaxLength\)

用动态规划解。设一个序列型动态规划f为以i-1位最后一位，是否可以组成一连续word

```
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
        n = len(s)
        f = [False for _ in xrange(n + 1)]
        f[0] = True
        maxLength = self.getMaxLength(wordDict)
        wordDict = self.convertToDict(wordDict)
        for i in xrange(1, n + 1):
            length = 0
            while i - length >= 0 and length <= maxLength:
                word = s[i - length:i]
                if word in wordDict and f[i - length]:
                    f[i] = True
                    break
                length += 1
        return f[n]
    def convertToDict(self, wordDict):
        hs = set([])
        for word in wordDict:
            hs.add(word)
        return hs
    def getMaxLength(self, wordDict):
        ans = 0
        for word in wordDict:
            ans = max(ans, len(word))
        return ans
```



