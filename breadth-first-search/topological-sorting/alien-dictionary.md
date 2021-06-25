Alien Dictionary 解题报告

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of **non-empty **words from the dictionary, where **words are sorted lexicographically by the rules of this new language**. Derive the order of letters in this language.

**Example 1:**  
Given the following words in dictionary,

```
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]
```

The correct order is:`"wertf"`.

**Example 2:**  
Given the following words in dictionary,

```
[
  "z",
  "x"
]
```

The correct order is:`"zx"`.

**Example 3:**  
Given the following words in dictionary,

```
[
  "z",
  "x",
  "z"
]
```

The order is invalid, so return`""`.

**Note:**

1. You may assume all letters are in lowercase.
2. You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
3. If the order is invalid, return an empty string.
4. There may be multiple valid order of letters, return any one of them is fine.

Idea:

先理解题意：

dictionary是按照word的顺序来的，就是说同一个word中字母之间没有顺序，这个顺序只体现在相邻的两个word之间有顺序。

再分析思路：

所以在dictionary当中两两单词比较，可以确定第一位不同的两个字母的顺序，即构造出有向图的一条边。那么这个题意就是说，把这个字典转换成有向图，判断这个有向图是否可以拓补排序，如果可以的话写出它的拓补排序。是否可以拓补排序可以通过最后ans的长度是否等于图中点的个数来判断

这个题目在实现的时候有两个比较tricky的地方

1.在图的构造时，我们将它分为两个部分，先遍历一遍保证把每个字符都插入图中，再遍历一遍确定边（也就是点之间的先后关系）。第一个阶段很容易被miss，那么构造的图就不完全，只包含了有边的点，没包含没边的点。

2.indegree的计算不能跟图构造一起进行，否则假设图的构造有连续n个单词都是连r-&gt;t，那么r-&gt;t被连了n次，实际上t只有一个入度但是放在一起写的话t会多出来n-1个入度，这样是不对的

```py
class Solution(object):
    def alienOrder(self, words):
        """
        :type words: List[str]
        :rtype: str
        """
        graph = self.getGraph(words)
        indegree = self.getIndegree(graph)
        q = []
        for node in indegree.keys():
            if indegree[node] == 0:
                q.append(node)
        ans = ''
        while q:
            tmp = q.pop(0)
            ans += tmp
            if tmp not in graph:
                continue
            for neighbor in graph[tmp]:
                if indegree[neighbor] == 1:
                    q.append(neighbor)
                indegree[neighbor] -= 1
        if len(ans) == len(graph):
            return ans
        return ""
    def getGraph(self, words):
        graph = {}
        n = len(words)
        for word in words:
            for j in xrange(len(word)):
                if word[j] not in graph:
                    graph[word[j]] = set([])
        for i in xrange(1, n):
            word1 = words[i - 1]
            word2 = words[i]
            j = 0
            while j < len(word1) and j < len(word2) and word1[j] == word2[j]:
                j += 1
            if j < len(word1) and j < len(word2):
                graph[word1[j]].add(word2[j])
        return graph
    def getIndegree(self, graph):
        indegree = {}
        for node in graph.keys():
            if node not in indegree:
                indegree[node] = 0
            for neighbor in graph[node]:
                if neighbor not in indegree:
                    indegree[neighbor] = 1
                else:
                    indegree[neighbor] += 1
        return indegree
```
