Add and Search Word - Data structure design 解题报告

Design a data structure that supports the following two operations:

```
void addWord(word)
bool search(word)
```

search\(word\) can search a literal word or a regular expression string containing only letters`a-z`or`.`. A`.`means it can represent any one letter.

For example:

```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```

**Note:**  
You may assume that all words are consist of lowercase letters`a-z`.

Idea:

因为'.'的存在需要递归，search的时候需要建立另外一个递归函数，递归函数的两个参量为word和当前node。遇到'.'则递归search其他剩下的。这个题目是一道带着当前trie node进行递归的题目。DFS in TrieTree

```
class WordDictionary(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()

    def addWord(self, word):
        """
        Adds a word into the data structure.
        :type word: str
        :rtype: void
        """
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.isWord = True
        
    def search(self, word):
        """
        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
        :type word: str
        :rtype: bool
        """
        return self.helper(word, self.root)
    def helper(self, word, node):
        if word == "":
            return node.isWord
        for i in xrange(len(word)):
            if word[i] == '.':
                for key in node.children.keys():
                    if self.helper(word[i + 1:], node.children[key]):
                        return True
                return False
            if word[i] not in node.children:
                return False
            node = node.children[word[i]]
        return node.isWord
        
class TrieNode:
    def __init__(self,):
        self.children = {}
        self.isWord = False

# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```



