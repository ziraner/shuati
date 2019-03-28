Connected Component in Undirected Graph 解题报告

Find the number connected component in the undirected graph. Each node in the graph contains a label and a list of its neighbors. \(a connected component \(or just component\) of an undirected graph is a subgraph in which any two vertices are connected to each other by paths, and which is connected to no additional vertices in the supergraph.\)

**Example**

Given graph:

```
A------B  C
 \     |  | 
  \    |  |
   \   |  |
    \  |  |
      D   E
```

Return`{A,B,D}, {C,E}`. Since there are two connected component which is`{A,B,D}, {C,E}`

这个题目两个思路：

思路一用unionfind跟weak connected component那个题一样考察的是以大哥为单位输出所有联通分量

```
class UnionFind:
    def __init__(self, graph):
        self.father = {}
        for node in graph:
            self.father[node] = node
    def find(self, a):
        if self.father[a] == a:
            return a
        self.father[a] = self.find(self.father[a])
        return self.father[a]
    def union(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b

class Solution:
    # @param {UndirectedGraphNode[]} nodes a array of undirected graph node
    # @return {int[][]} a connected set of a undirected graph
    def connectedSet(self, nodes):
        # Write your code here
        graph = set([])
        for node in nodes:
            graph.add(node)
            for neighbor in node.neighbors:
                graph.add(node)
        uf = UnionFind(graph)
        for node in nodes:
            for neighbor in node.neighbors:
                uf.union(node, neighbor)
        f = {}
        for node in nodes:
            father = uf.find(node)
            if father.label not in f:
                f[father.label] = [node.label]
            else:
                f[father.label].append(node.label)
        ans = []
        for key in f.keys():
            ans.append(f[key][:])
        return ans
```

第二个思路是图中的由点及面的BFS

```
class Solution:
    # @param {UndirectedGraphNode[]} nodes a array of undirected graph node
    # @return {int[][]} a connected set of a undirected graph
    def connectedSet(self, nodes):
        if not nodes:
            return []

        visited = set([])
        result = []

        for node in nodes:
            if node not in visited:
                self.bfs(nodes, node, visited, result)
        return result

    def bfs(self, nodes, start, visited, result):
        queue = [start]
        visited.add(start)
        connected = []
        while queue:
            tmp = queue.pop(0)
            connected.append(tmp.label)
            for neighbor in tmp.neighbors:
                if neighbor in visited:
                    continue
                visited.add(neighbor)
                queue.append(neighbor)
        connected = sorted(connected)
        result.append(connected[:])
```



