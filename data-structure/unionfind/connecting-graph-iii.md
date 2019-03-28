Connecting Graph III 解题报告

Given`n`nodes in a graph labeled from`1`to`n`. There is no edges in the graph at beginning.

You need to support the following method:  
1.`connect(a, b)`, an edge to connect node a and node b  
2.`query()`, Returns the number of connected component in the graph

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

这个题目要求返回整体孤岛的数量

```
class ConnectingGraph3:
    """
    @param: n: An integer
    """
    def __init__(self, n):
        # do intialization if necessary
        self.count = n
        self.father = [i for i in xrange(n + 1)]

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
            self.count -= 1
            self.father[root_a] = root_b

    """
    @return: An integer
    """
    def query(self, ):
        # write your code here
        return self.count

    def find(self, a):
        if self.father[a] == a:
            return a
        self.father[a] = self.find(self.father[a])
        return self.father[a]
```



