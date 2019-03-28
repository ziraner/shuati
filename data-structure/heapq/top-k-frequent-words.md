Top K Frequent Words 解题报告

Given a list of words and an integer k, return the top k frequent words in the list.

##### Notice

You should order the words by the frequency of them in the return list, the most frequent one comes first. If two words has the same frequency, the one with lower alphabetical order come first.

**Example**

Given

```
[
    "yes", "lint", "code",
    "yes", "code", "baby",
    "you", "baby", "chrome",
    "safari", "lint", "code",
    "body", "lint", "code"
]

```

for k =`3`, return`["code", "lint", "baby"]`.

for k =`4`, return`["code", "lint", "baby", "yes"]`

Idea：

这个题目tricky的地方在于，如果用O\(nlogk\)time，O\(k\)space的方法，即用heapq来做：题目要求返回最大的freq，如果freq相同则按照字母小到大排序，这个跟heap里面的自动排序是相反的；我们把pair（freq，word）放进heap是不对的，因为是minheap每次弹出来最小的freq，如果freq相同则弹出来最小的word，是不对的因为如果abc和cba两个单词freq一样应该淘汰的是cba而不是abc；所以freq是小的在前和word是大的在前，它俩的排序是拧着来的，所以我们需要建立一个Pair的type，override里面的_cmp_函数

或者可以直接用sort来做，那么需要O\(n\)的space，O\(nlogn\)的time

```
class Solution(object):
    def topKFrequent(self, words, k):
        """
        :type words: List[str]
        :type k: int
        :rtype: List[str]
        """
        hm = {}
        for word in words:
            if word not in hm:
                hm[word] = 1
            else:
                hm[word] += 1
        h = []
        import heapq
        for word in hm.keys():
            if len(h) < k:
                heapq.heappush(h, Pair(word, hm[word]))
            else:
                if Pair(word, hm[word]) > h[0]:
                    heapq.heappop(h)
                    heapq.heappush(h, Pair(word, hm[word]))
        ans = []
        while h:
            ans.append(heapq.heappop(h).word)
        return ans[::-1]
class Pair:
    def __init__(self, word, freq):
        self.word = word
        self.freq = freq
    def __cmp__(self, other):
        if self.freq == other.freq:
            if self.word < other.word:
                return 1
            if self.word > other.word:
                return -1
            return 0
        return self.freq - other.freq
```



