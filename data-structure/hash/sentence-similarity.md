Sentence Similarity 解题报告

Given two sentences`words1, words2`\(each represented as an array of strings\), and a list of similar word pairs`pairs`, determine if two sentences are similar.

For example, "great acting skills" and "fine drama talent" are similar, if the similar word pairs are`pairs = [["great", "fine"], ["acting","drama"], ["skills","talent"]]`.

Note that the similarity relation is not transitive. For example, if "great" and "fine" are similar, and "fine" and "good" are similar, "great" and "good" are**not**necessarily similar.

However, similarity is symmetric. For example, "great" and "fine" being similar is the same as "fine" and "great" being similar.

Also, a word is always similar with itself. For example, the sentences`words1 = ["great"], words2 = ["great"], pairs = []`are similar, even though there are no specified similar word pairs.

Finally, sentences can only be similar if they have the same number of words. So a sentence like`words1 = ["great"]`can never be similar to`words2 = ["doubleplus","good"]`.

**Note:**

The length of`words1`and`words2`will not exceed`1000`.

The length of`pairs`will not exceed`2000`.

The length of each`pairs[i]`will be`2`.

The length of each`words[i]`and`pairs[i][j]`will be in the range`[1, 20]`.

Idea:

因为similar不具备transitive特性则比较简单，直接用用hashmap做就可以了。对每个pairs将word1加入word2为key的hm中，word2加入word1为key的hm中。

```
class Solution(object):
    def areSentencesSimilar(self, words1, words2, pairs):
        """
        :type words1: List[str]
        :type words2: List[str]
        :type pairs: List[List[str]]
        :rtype: bool
        """
        n = len(words1)
        if n != len(words2):
            return False
        sim = {}
        for word1, word2 in pairs:
            if word1 in sim:
                sim[word1].add(word2)
            else:
                sim[word1] = set([word2])
            if word2 in sim:
                sim[word2].add(word1)
            else:
                sim[word2] = set([word1])
        for i in xrange(n):
            word1, word2 = words1[i], words2[i]
            if word1 == word2:
                continue
            if word1 in sim and word2 in sim[word1]:
                continue
            if word2 in sim and word1 in sim[word2]:
                continue
            return False
        return True
```



