Sentence Similarity II 解题报告

Given two sentences`words1, words2`\(each represented as an array of strings\), and a list of similar word pairs`pairs`, determine if two sentences are similar.

For example,`words1 = ["great", "acting", "skills"]`and`words2 = ["fine", "drama", "talent"]`are similar, if the similar word pairs are`pairs = [["great", "good"], ["fine", "good"], ["acting","drama"], ["skills","talent"]]`.

Note that the similarity relation**is**transitive. For example, if "great" and "good" are similar, and "fine" and "good" are similar, then "great" and "fine"**are similar**.

Similarity is also symmetric. For example, "great" and "fine" being similar is the same as "fine" and "great" being similar.

Also, a word is always similar with itself. For example, the sentences`words1 = ["great"], words2 = ["great"], pairs = []`are similar, even though there are no specified similar word pairs.

Finally, sentences can only be similar if they have the same number of words. So a sentence like`words1 = ["great"]`can never be similar to`words2 = ["doubleplus","good"]`.

**Note:**

The length of`words1`and`words2`will not exceed`1000`.

The length of`pairs`will not exceed`2000`.

The length of each`pairs[i]`will be`2`.

The length of each`words[i]`and`pairs[i][j]`will be in the range`[1, 20]`.

Idea：

这个题目是Sentence Similarity的follow-up因为具有transitive特性就不能再直接用hashmap做了因为a和b相似，b和c相似，那么a和c也相似了，类似于一个相似的bfs过程，因为bfs会特别复杂且不太好写，则想到了用unionfind，将相似的俩俩union，那么transitive特性所有相似的肯定有一个共同的大哥

```
class Solution(object):
    def areSentencesSimilarTwo(self, words1, words2, pairs):
        """
        :type words1: List[str]
        :type words2: List[str]
        :type pairs: List[List[str]]
        :rtype: bool
        """
        n = len(words1)
        if len(words2) != n:
            return False
        uf = UnionFind()
        for word1, word2 in pairs:
            uf.insert(word1)
            uf.insert(word2)
            uf.union(word1, word2)
        for i in xrange(n):
            word1, word2 = words1[i], words2[i]
            if word1 == word2:
                continue
            if word1 not in uf.father or word2 not in uf.father:
                return False
            if uf.find(word1) != uf.find(word2):
                return False
        return True
class UnionFind:
    def __init__(self, ):
        self.father = {}
    def insert(self, word):
        if word not in self.father:
            self.father[word] = word
    def union(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b
    def find(self, a):
        if a == self.father[a]:
            return a
        self.father[a] = self.find(self.father[a])
        return self.father[a]
```



