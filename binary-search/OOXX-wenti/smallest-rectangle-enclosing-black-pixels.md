Lintcode 600: Smallest Rectangle Enclosing Black Pixels \(HD\) 解题报告

Problem:

An image is represented by a binary matrix with`0`as a white pixel and`1`as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location`(x, y)`of one of the black pixels, return the area of the smallest \(axis-aligned\) rectangle that encloses all black pixels.

Example:

For example, given the following image:

```
[
  "0010",
  "0110",
  "0100"
]
```

and x =`0`, y =`2`,  
Return`6`.

Idea:  
1. The Idea is that the smallest rectangle is sth like: OOOXXXOOO for both row & column:  find the leftbound & rightbound for XXX in both row & column

1. How to write the check function: given a row/column position, check if the entire row/column is zero

```
class Solution(object):
    # @param image {List[List[str]]}  a binary matrix with '0' and '1'
    # @param x, y {int} the location of one of the black pixels
    # @return an integer
    def minArea(self, image, x, y):
        # Write your code here
        # O(nlogn)
        if not image or not image[0]:
            return 0
        l = self.findLeft(image, 0, y)
        r = self.findRight(image, y, len(image[0]) - 1)
        u = self.findUp(image, 0, x)
        b = self.findBottom(image, x, len(image) - 1)
        return (r - l + 1) * (b - u + 1)
    def findLeft(self, image, start, end):
        while start + 1 < end:
            mid = (start + end) / 2
            if self.checkCol(image, mid):
                start = mid
            else:
                end = mid
        if not self.checkCol(image, start):
            return start
        return end
    def findRight(self, image, start, end):
        while start + 1 < end:
            mid = (start + end) / 2
            if self.checkCol(image, mid):
                end = mid
            else:
                start = mid
        if not self.checkCol(image, end):
            return end
        return start
    def findUp(self, image, start, end):
        while start + 1 < end:
            mid = (start + end) / 2
            if self.checkRow(image, mid):
                start = mid
            else:
                end = mid
        if not self.checkRow(image, start):
            return start
        return end
    def findBottom(self, image, start, end):
        while start + 1 < end:
            mid = (start + end) / 2
            if self.checkRow(image, mid):
                end = mid
            else:
                start = mid
        if not self.checkRow(image, end):
            return end
        return start
    def checkRow(self, image, x):
        for j in xrange(len(image[x])):
            if image[x][j] == '1':
                return False
        return True
    def checkCol(self, image, y):
        for i in xrange(len(image)):
            if image[i][y] == '1':
                return False
        return True
```



