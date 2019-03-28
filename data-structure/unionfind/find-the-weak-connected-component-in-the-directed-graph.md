Find the Weak Connected Component in the Directed Graph 解题报告

Find the number Weak Connected Component in the directed graph. Each node in the graph contains a label and a list of its neighbors. \(a connected set of a directed graph is a subgraph in which any two vertices are connected by direct edge path.\)

**Example**

Given graph:

```
A----->B  C
 \     |  | 
  \    |  |
   \   |  |
    \  v  v
     ->D  E <- F
```

Return`{A,B,D}, {C,E,F}`. Since there are two connected component which are`{A,B,D} and {C,E,F}`

Idea:

弱联通分量是有向图转换成无向图时候的联通分量

这个题目考察在union find中以联通分量为单位output所有的点

第一步建立图，然后用这个图set去initialize unionfind

第二步链接图的边在unionfind中

第三步对每个点找一下unionfind中它的大哥，这样可以把所有点都指向大哥。且可以把大哥相同的联通分量记录在以大哥为key的hashmap中

第四步遍历hashmap输出各大哥的联通分量都是谁 即答案

```
class UnionFind:
    def __init__(self, hs):
        self.father = {}
        for node in hs:
            self.father[node] = node
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

class Solution:
    """
    @param: nodes: a array of Directed graph node
    @return: a connected set of a directed graph
    """
    def connectedSet2(self, nodes):
        # write your code here
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



