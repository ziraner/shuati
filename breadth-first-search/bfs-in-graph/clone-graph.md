Clone Graph 解题报告

Clone an undirected graph. Each node in the graph contains a`label`and a list of its`neighbors`.

Idea:

先BFS，由点及面找到所有nodes

再对每一个旧node，create一个对应的新node，并把mapping保存起来

最后把新node的neighbor connect起来

```
# Definition for a undirected graph node
# class UndirectedGraphNode:
#     def __init__(self, x):
#         self.label = x
#         self.neighbors = []

class Solution:
    # @param node, a undirected graph node
    # @return a undirected graph node
    def cloneGraph(self, node):
        if not node:
            return None
        graph = self.bfs(node)
        hm = {}
        for old_node in graph:
            hm[old_node] = UndirectedGraphNode(old_node.label)
        for old_node in graph:
            new_node = hm[old_node]
            for neighbor in old_node.neighbors:
                new_neighbor = hm[neighbor]
                new_node.neighbors.append(new_neighbor)
        return hm[node]
        
    def bfs(self, node):
        visited = set([node])
        q = [node]
        while q:
            tmp = q.pop(0)
            for neighbor in tmp.neighbors:
                if neighbor in visited:
                    continue
                q.append(neighbor)
                visited.add(neighbor)
        return visited
```



