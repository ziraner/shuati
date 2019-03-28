Implement Magic Dictionary 解题报告

Implement a magic directory with`buildDict`, and`search`methods.

For the method`buildDict`, you'll be given a list of non-repetitive words to build a dictionary.

For the method`search`, you'll be given a word, and judge whether if you modify**exactly**one character into**another**character in this word, the modified word is in the dictionary you just built.

**Example 1:**

```
Input: buildDict(["hello", "leetcode"]), Output: Null
Input: search("hello"), Output: False
Input: search("hhllo"), Output: True
Input: search("hell"), Output: False
Input: search("leetcoded"), Output: False
```

**Note:**

1. You may assume that all the inputs are consist of lowercase letters`a-z`.
2. For contest purpose, the test data is rather small by now. You could think about highly efficient algorithm after the contest.
3. Please remember to **RESET **your class variables declared in class MagicDictionary, as static/class variables are **persisted across multiple test cases**

Idea:

用Trie。

感觉像是add and search word和valid palindrome II结合体。写两个函数，一个是isMatch一个是isOneEdit，其中isOneEdit是一个递归函数，他们两个的input都是word和当前的node。而search的input只有一个word，search去调用isOneEdit，然后isOneEdit分情况讨论:1 . 第一个字符change，调用isMatch;2. 非第一个字符change，则递归调用自己。

```
class MagicDictionary(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()

    def buildDict(self, dict):
        """
        Build a dictionary through a list of words
        :type dict: List[str]
        :rtype: void
        """
        for word in dict:
            self.insert(word)

    def insert(self, word):
        if not word:
            return
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.isWord = True

    def isMatch(self, word, node):
        for c in word:
            if c not in node.children:
                return False
            node = node.children[c]
        return node.isWord

    def isOneEdit(self, word, node):
        if word == '':
            return False
        digit = word[0]
        for c in node.children:
            if c != digit:
                if self.isMatch(word[1:], node.children[c]):
                    return True
        if digit not in node.children:
            return False
        return self.isOneEdit(word[1:], node.children[digit])

    def search(self, word):
        """
        Returns if there is any word in the trie that equals to the given word after modifying exactly one character
        :type word: str
        :rtype: bool
        """
        return self.isOneEdit(word, self.root)    

class TrieNode:
    def __init__(self, ):
        self.children = {}
        self.isWord = False

# Your MagicDictionary object will be instantiated and called as such:
# obj = MagicDictionary()
# obj.buildDict(dict)
# param_2 = obj.search(word)
```



