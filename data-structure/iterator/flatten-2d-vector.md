Flatten 2D Vector 解题报告

Implement an iterator to flatten a 2d vector.

For example,  
Given 2d vector =

```
[
  [1,2],
  [3],
  [4,5,6]
]
```

By callingnextrepeatedly untilhasNextreturns false, the order of elements returned bynextshould be:`[1,2,3,4,5,6]`.

Idea：

方法一：在intialization里面写逻辑

```
class Vector2D(object):

    # @param vec2d {List[List[int]]}
    def __init__(self, vec2d):
        # Initialize your data structure here
        self.vec = []
        for v in vec2d:
            self.vec += v
        self.index = 0

    # @return {int} a next element
    def next(self):
        # Write your code here
        if not self.hasNext():
            return None
        val = self.vec[self.index]
        self.index += 1
        return val

    # @return {boolean} true if it has next element
    # or false
    def hasNext(self):
        # Write your code here
        return self.index != len(self.vec)
        

# Your Vector2D object will be instantiated and called as such:
# i, v = Vector2D(vec2d), []
# while i.hasNext(): v.append(i.next())
```

方法二：在hasNext里面写逻辑

```
class Vector2D(object):

    def __init__(self, vec2d):
        """
        Initialize your data structure here.
        :type vec2d: List[List[int]]
        """
        self.row, self.col, self.vec = 0, 0, vec2d

    def next(self):
        """
        :rtype: int
        """
        val = 0
        if self.hasNext():
            val = self.vec[self.row][self.col]
            self.col += 1
        return val
            

    def hasNext(self):
        """
        :rtype: bool
        """
        while self.row < len(self.vec) and self.col >= len(self.vec[self.row]):
            self.row, self.col = self.row + 1, 0
        return self.row < len(self.vec)

# Your Vector2D object will be instantiated and called as such:
# i, v = Vector2D(vec2d), []
# while i.hasNext(): v.append(i.next())
```



