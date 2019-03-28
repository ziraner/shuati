Topological Sorting 解题报告

Given an directed graph, a topological order of the graph nodes is defined as follow:

* For each directed edge`A -> B`in graph, A must before B in the order list.
* The first node in the order can be any node in the graph with no nodes direct to it.

Find any topological order for the given graph.

##### Notice

You can assume that there is at least one topological order in the graph.

**Example**

For graph as follow:

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcThE9AgZZszyhwe0o9qpp3VyizdIj9kWwMY50HiQEysXvkSLsoZ "picture")

The topological order can be:

```
[0, 1, 2, 3, 4, 5]
[0, 2, 3, 1, 5, 4]
...
```

Idea:  
拓补排序可能是面试考的为数不多有向图题目的热门。构造一个indegree的hashmap记录每个node的indegree，没有在hashmap中的node即为indegree为0的node；BFS的时候每加入一个q中node的neighbor，将该node的indegree减一；将indegree减为0的node加入q

```
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



