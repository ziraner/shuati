K Edit Distance 解题报告

Given a set of strings which just has lower case letters and a target string, output all the strings for each the edit distance with the target no greater than`k`.

You have the following 3 operations permitted on a word:

* Insert a character
* Delete a character
* Replace a character

**Example**

Given words =`["abc", "abd", "abcd", "adc"]`and target =`"ac"`, k =`1`  
Return`["abc", "adc"]`

正常的匹配类DP，套用edit distance的思路并不能过AC时间复杂度O\(N \* length\(longest word\) \* length\(target\)\) 过不了AC

```
class Solution:
    """
    @param: words: a set of stirngs
    @param: target: a target string
    @param: k: An integer
    @return: output all the strings that meet the requirements
    """    
    def kDistance(self, words, target, k):
        # write your code here
        """
        ans = []
        for word in words:
            if self.minDistance(word, target) <= k:
                ans.append(word)
        return ans
    def minDistance(self, s1, s2):
        n1, n2 = len(s1), len(s2)
        dp = [[0 for _ in range(n2 + 1)] for _ in range(n1 + 1)]
        dp[0][0] = 0
        for i in range(1, n1 + 1):
            dp[i][0] = i
        for j in range(1, n2 + 1):
            dp[0][j] = j
        for i in range(1, n1 + 1):
            for j in range(1, n2 + 1):
                if s1[i - 1] == s2[j - 1]:
                    dp[i][j] = min(dp[i - 1][j - 1], dp[i][j - 1] + 1, dp[i - 1][j] + 1)
                else:
                    dp[i][j] = min(dp[i - 1][j - 1], dp[i][j - 1], dp[i - 1][j]) + 1
        return dp[n1][n2]
```

需要加入trie 来优化  
将words填进trie，然后用rolling 2D array从trie的root向下走。比较的就是当前的node不论已经走过了多少个node，匹配上target上的每一位，的最小的edit，因为trie中每个node最多有26个，所以时间复杂度是O\(26\*len\(target\)\*longestlength\(words\)\)

```
class Solution:
    """
    @param: words: a set of stirngs
    @param: target: a target string
    @param: k: An integer
    @return: output all the strings that meet the requirements
    """
    def kDistance(self, words, target, k):
        # write your code here
        # trie tree version: O(26 * Height(TrieTree) * Length(target))
        trie = TrieTree(words)
        self.ans = []
        # dp[0][j] = j: init of first row
        dp = [i for i in range(len(target) + 1)]
        self.search(trie.root, dp, target, k)
        return self.ans
    def search(self, node, dp, target, k):
        n = len(target)
        if node.isWord and dp[n] <= k:
            self.ans.append(node.word)
        next_dp = [0 for _ in range(n + 1)]
        for c in node.children.keys():
            new_node = node.children[c]
            #dp[i%2] is next_dp, dp[(i-1)%2] is dp
            #dp[i%2][0] = dp[(i-1)%2][0] + 1: init of first column
            next_dp[0] = dp[0] + 1
            for j in range(1, n + 1):
                if target[j - 1] == c:
                    #dp[i%2][j] = min(dp[(i-1)%2][j-1], dp[(i-1)%2][j]+1, dp[i%2][j-1]+1)
                    next_dp[j] = min(dp[j - 1], dp[j] + 1, next_dp[j - 1] + 1)
                else:
                    #dp[i%2][j] = min(dp[(i-1)%2][j-1], dp[(i-1)%2][j], dp[i%2][j-1])+1
                    next_dp[j] = min(dp[j - 1], dp[j], next_dp[j - 1]) + 1
            self.search(new_node, next_dp, target, k)
class TrieNode:
    def __init__(self, ):
        self.isWord = False
        self.children = {}
        self.word = ""
class TrieTree:
    def __init__(self, words):
        self.root = TrieNode()
        for word in words:
            self.insert(word)
    def insert(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.isWord = True
        node.word = word
```



