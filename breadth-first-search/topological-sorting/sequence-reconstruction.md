Sequence Reconstruction 解题报告

Check whether the original sequence`org`can be uniquely reconstructed from the sequences in`seqs`. The org sequence is a permutation of the integers from 1 to n, with 1 ≤ n ≤ 10^4. Reconstruction means building a shortest common supersequence of the sequences in`seqs`\(i.e., a shortest sequence so that all sequences in`seqs`are subsequences of it\). Determine whether there is only one sequence that can be reconstructed from`seqs`and it is the`org`sequence.

**Example**

```
Given org = [1,2,3], seqs = [[1,2],[1,3]]
Return false
Explanation:
[1,2,3] is not the only one sequence that can be reconstructed, because [1,3,2] is also a valid sequence that can be reconstructed.

Given org = [1,2,3], seqs = [[1,2]]
Return false
Explanation:
The reconstructed sequence can only be [1,2].

Given org = [1,2,3], seqs = [[1,2],[1,3],[2,3]]
Return true
Explanation:
The sequences [1,2], [1,3], and [2,3] can uniquely reconstruct the original sequence [1,2,3].

Given org = [4,1,5,2,6,3], seqs = [[5,2,6,3],[4,1,5,2]]
Return true
```

Idea:

拓补排序问题。

用构造成一个adjList和一个indegree hashmap

做BFS将indegree为0的元素放入q

原题为True的条件：1. 做BFS时任何时候q中只能有一个元素 2. BFS构造出来的seq和org相等

```
class Solution(object):
    def sequenceReconstruction(self, org, seqs):
        """
        :type org: List[int]
        :type seqs: List[List[int]]
        :rtype: bool
        """
        adjList, indegree = {}, {}
        for seq in seqs:
            for i in xrange(len(seq)):
                if i == 0:
                    if seq[i] in indegree: indegree[seq[i]] += 0
                    else: indegree[seq[i]] = 0
                else:
                    if seq[i] in indegree: indegree[seq[i]] += 1
                    else: indegree[seq[i]] = 1
                    if seq[i - 1] in adjList: adjList[seq[i - 1]].append(seq[i])
                    else: adjList[seq[i - 1]] = [seq[i]]
        if set(indegree.keys()) != set(org):
            return False
        q = []
        for key in indegree.keys():
            if indegree[key] == 0:
                q.append(key)
        ans = []
        while q:
            tmp = q.pop(0)
            ans.append(tmp)
            if len(q) != 0:
                return False
            if tmp not in adjList:
                break
            for neighbor in adjList[tmp]:
                indegree[neighbor] -= 1
                if indegree[neighbor] == 0:
                    q.append(neighbor)
        return ans == org
```



