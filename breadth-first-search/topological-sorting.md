图的拓补排序可能是有向图的唯一考察点

数据结构:
Queue + graph的表达方式（要么是一个存边edges的list要么是一个图的adjacency list）+ indegree hashmap: Map<Node, Integer>

实现方法：
1. 算出图中每个node的indegree保存在indegree hashmap中
2. 把所有indegree为0的进Queue
3. bfs Queue中的node，把跟该node相邻的node的indegree都减一，然后把indegree为0的重新入Queue

应用：
一般不会裸考拓补排序，一切跟任何东西的先后顺序有紧密关联的题目都可以考虑一下拓补排序
1. 上课的先后顺序：course schedule I & II
2. 字符串中字符的先后顺序：sequence reconstruction
3. 字典中单词（字母）的先后顺序：alien dictionary

**Topological Sorting**
```py
# Definition for a Directed graph node
# class DirectedGraphNode:
#     def __init__(self, x):
#         self.label = x
#         self.neighbors = []

class Solution:
    """
    @param graph: A list of Directed graph node
    @return: A list of graph nodes in topological order.
    """
    def topSort(self, graph):
        # write your code here
        # get a map of non-zero indegree nodes
        if not graph:
            return []
        hm = self.getIndegree(graph)
        q = []
        for v in graph:
            if v not in hm:
                q.append(v)
        ans = []
        while q:
            tmp = q.pop(0)
            ans.append(tmp)
            for neighbor in tmp.neighbors:
                if hm[neighbor] == 1:
                    q.append(neighbor)
                hm[neighbor] -= 1
        return ans

    def getIndegree(self, graph):
        indegree_map = {}
        for v in graph:
            for neighbor in v.neighbors:
                if neighbor in indegree_map:
                    indegree_map[neighbor] += 1
                else:
                    indegree_map[neighbor] = 1
        return indegree_map
```
