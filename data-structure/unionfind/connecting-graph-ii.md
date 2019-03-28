Connecting Graph II 解题报告

Given`n`nodes in a graph labeled from`1`to`n`. There is no edges in the graph at beginning.

You need to support the following method:  
1.`connect(a, b)`, an edge to connect node a and node b  
2.`query(a)`, Returns the number of connected component nodes which include node`a`.

**Example**

```
5 // n = 5
query(1) return 1
connect(1, 2)
query(1) return 2
connect(2, 4)
query(1) return 3
connect(1, 4)
query(1) return 3

```

这个题目的意思是query一个点的时候，返回它大哥节点的联通的点的数量。联通点数量在两个大哥节点合并的时候更新。  
query的点不是大哥节点的话需要先找到大哥节点然后返回大哥节点的联通数量

```
class ConnectingGraph2:
    """
    @param: n: An integer
    """
    def __init__(self, n):
        # do intialization if necessary
        self.father = [i for i in range(n + 1)]
        self.count = [1 for _ in range(n + 1)]

    """
    @param: a: An integer
    @param: b: An integer
    @return: nothing
    """
    def connect(self, a, b):
        # write your code here
        root_a = self.find(a)
        root_b = self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b
            self.count[root_b] += self.count[root_a]
    """
    @param: a: An integer
    @return: An integer
    """
    def query(self, a):
        # write your code here
        root_a = self.find(a)
        return self.count[root_a]

    def find(self, a):
        if self.father[a] == a:
            return a
        self.father[a] = self.find(self.father[a])
        return self.father[a]
```



