Graph Valid Tree 解题报告

Given`n`nodes labeled from`0`to`n - 1`and a list of undirected edges \(each edge is a pair of nodes\), write a function to check whether these edges make up a valid tree.

For example:

Given`n = 5`and`edges = [[0, 1], [0, 2], [0, 3], [1, 4]]`, return`true`.

Given`n = 5`and`edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]`, return`false`.

**Note**: you can assume that no duplicate edges will appear in`edges`. Since all edges are undirected,`[0, 1]`is the same as`[1, 0]`and thus will not appear together in`edges`.

思路：树的话1. 是没有环的所以假设有n个点只能有n - 1条边 2. 所有的点之间都是联通的 满足以上两个条件是树无疑

方法一：基于图的BFS

先判断edges的数量是n - 1。然后通过edges构造图的adjacency list，做基于图的BFS，最后判断BFS中所有联通分量的个数是否为n

```python
class Solution(object):
    def validTree(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: bool
        """
        graph = self.graphInit(edges)
        if len(edges) != n - 1:
            return False
        q, visited = [0], set([0])
        while q:
            tmp = q.pop(0)
            if tmp not in graph:
                continue
            for neighbor in graph[tmp]:
                if neighbor in visited:
                    continue
                q.append(neighbor)
                visited.add(neighbor)
        return len(visited) == n
    def graphInit(self, edges):
        graph = {}
        for u, v in edges:
            if u in graph:
                graph[u].append(v)
            else:
                graph[u] = [v]
            if v in graph:
                graph[v].append(u)
            else:
                graph[v] = [u]
        return graph
```

```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (n == 0 || edges.length != n -1)
            return false;

        Map<Integer, Set<Integer>> graph = initializeGraph(n, edges);
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();

        queue.offer(0);
        visited.add(0);
        while (!queue.isEmpty()) {
            int node = queue.poll();
            for (Integer neighbor : graph.get(node)) {
                if (visited.contains(neighbor)) continue;
                queue.offer(neighbor);
                visited.add(neighbor);
            }
        }
        return visited.size() == n;
    }

    private Map<Integer, Set<Integer>> initializeGraph(int n, int[][] edges) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<>());
        }

        for (int i = 0; i < edges.length; i++) {
            graph.get(edges[i][0]).add(edges[i][1]);
            graph.get(edges[i][1]).add(edges[i][0]);
        }
        return graph;
    }
}
```

方法二：union find

先判断edges的数量是n - 1。然后将边两两联通，在联通之前如果这两个点已经联通了说明有环，不能构成树，否则则可以构成树

```py
class Solution(object):
    def validTree(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: bool
        """
        if n - 1 != len(edges) or n <= 0:
            return False
        uf = UnionFind(n)
        for u, v in edges:
            # before u, v union, they cannot be connected, otherwise it's a loop
            if uf.find(u) == uf.find(v):  
                return False
            uf.union(u, v)
        return True
class UnionFind:
    def __init__(self, n):
        self.father = [i for i in xrange(n)]
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
```

```java
class Solution {
    class UnionFind {
        Map<Integer, Integer> father = new HashMap<>();
        UnionFind(int n) {
            for (int i = 0; i < n; i++) {
                father.put(i, i);
            }
        }

        int compressed_find(int x) {
            int parent = x;
            while (parent != father.get(parent)) {
                parent = father.get(parent);
            }

            int temp = Integer.MIN_VALUE;
            int fa = x;
            while (fa != father.get(fa)) {
                temp = father.get(fa);
                father.put(fa, parent);
                fa = temp;
            }
            return parent;
        }

        void union(int x, int y) {
            int fa_x = compressed_find(x);
            int fa_y = compressed_find(y);
            if (fa_x != fa_y) {
                father.put(fa_x, fa_y);
            }
        }
    }

    public boolean validTree(int n, int[][] edges) {
        if (n == 0 || edges.length != n - 1) {
            return false;
        }

        UnionFind uf = new UnionFind(n);
        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            if (uf.compressed_find(u) == uf.compressed_find(v)) {
                return false;
            }
            uf.union(u, v);
        }

        return true;
    }
}
```
