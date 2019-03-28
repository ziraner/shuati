Connecting Graph 解题报告

Given`n`nodes in a graph labeled from`1`to`n`. There is no edges in the graph at beginning.

You need to support the following method:  
1.`connect(a, b)`, add an edge to connect node`a`and node b`. 2.`query\(a, b\)\`, check if two nodes are connected

Idea:

UnionFind 裸考题目 Lintcode自己的题目

这个题目是判断两个点是否联通的，这个判断条件在一些题目中作为if语句的判断条件很有用

```
class ConnectingGraph:
    """
    @param: n: An integer
    """
    def __init__(self, n):
        # do intialization if necessary
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
            self.father[root_a] = root_b

    """
    @param: a: An integer
    @param: b: An integer
    @return: A boolean
    """
    def query(self, a, b):
        # write your code here
        return self.find(a) == self.find(b)

    def find(self, a):
        if a == self.father[a]:
            return a
        self.father[a] = self.find(self.father[a])
        return self.father[a]
```



