Edit Distance 解题报告

Given two words_word1_and_word2_, find the minimum number of steps required to convert word1 to word2. \(each operation is counted as 1 step.\)

You have the following 3 operations permitted on a word:

* Insert a character
* Delete a character
* Replace a character

匹配型DP

```
class Solution(object):
    def minDistance(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: int
        """
        m, n = len(word1), len(word2)
        f = [[0 for _ in xrange(n + 1)] for _ in xrange(m + 1)]
        for i in xrange(m + 1):
            f[i][0] = i
        for j in xrange(n + 1):
            f[0][j] = j
        for i in xrange(1, m + 1):
            for j in xrange(1, n + 1):
                if word1[i - 1] == word2[j - 1]:
                    f[i][j] = min(f[i - 1][j - 1], f[i][j - 1] + 1, f[i - 1][j] + 1)
                else:
                    f[i][j] = min(f[i - 1][j - 1], f[i][j - 1], f[i - 1][j]) + 1
        return f[m][n]

```



