K Closest Points 解题报告

Given some`points`and a point`origin`in two dimensional space, find`k`points out of the some points which are nearest to`origin`.  
Return these points sorted by distance, if they are same with distance, sorted by x-axis, otherwise sorted by y-axis.

**Example**

Given points =`[[4,6],[4,7],[4,4],[2,5],[1,1]]`, origin =`[0, 0]`, k =`3`  
return`[[1,1],[2,5],[4,4]]`

思路：

这个题目tricky的地方要求按照distance排序，如果distance相同按照x坐标排序，如果x坐标相同按照y排序。

第一种思路是自己建一个类型，然后override它的比较函数。跟alphabetsort不同的地方在于，这个cmp函数是类型里面的override， 然后可以直接把类型加入到heap中

这里其实上是一个最大堆，但是因为可以override cmp函数，我们改变它的方向，形成dist最小堆，x和y的最小堆also

```
from heapq import heappush, heappop
class PointType:
    def __init__(self, point, dist):
        self.point = point
        self.dist = dist
    def __cmp__(self, other):
        if self.dist == other.dist:
            if self.point.x == other.point.x:
                return other.point.y - self.point.y
            return other.point.x - self.point.x
        return other.dist - self.dist
class Solution:
    """
    @param: points: a list of points
    @param: origin: a point
    @param: k: An integer
    @return: the k closest points
    """
    def kClosest(self, points, origin, k):
        # write your code here
        hpq = []
        for point in points:
            dist = self.getDistance(point, origin)
            if len(hpq) < k:
                heappush(hpq, PointType(point, dist))
            else:
                if dist < hpq[0].dist:
                    heappush(hpq, PointType(point, dist))
                    heappop(hpq)
        ans = []
        while len(hpq) != 0:
            ans.append(heappop(hpq).point)
        ans.reverse()
        return ans

    def getDistance(self, point, origin):
        return (point.x - origin.x) ** 2 + (point.y - origin.y) ** 2
```

或者利用python里面heapq里面存tuple的特性，把\(dist, x, y\)当成tuple存heapq里面然后会自动按照要求排序的。

```
class Solution:
    """
    @param: points: a list of points
    @param: origin: a point
    @param: k: An integer
    @return: the k closest points
    """
    def kClosest(self, points, origin, k):
        # write your code here
        import heapq
        h = []
        for point in points:
            dist = self.getDistance(point, origin)
            heapq.heappush(h, (dist, point.x, point.y))
        tmp = heapq.nsmallest(k, h)
        ans = []
        while tmp:
            _, x, y = heapq.heappop(tmp)
            ans.append(Point(x, y))
        return ans

    def getDistance(self, point, origin):
        return (point.x - origin.x) ** 2 + (point.y - origin.y) ** 2
```

如果不能用nsmallest或者nlargest，则可以用人造最大堆，把tuple放进去

```
class Solution:
    def kClosest(self, points, origin, k):        
        import heapq
        h = []
        for point in points:
            dist = self.getDistance(point, origin)
            if len(h) < k:
                heapq.heappush(h, (-dist, -point.x, -point.y))
            else:
                if (-dist, -point.x, -point.y) > h[0]:
                    heapq.heappush(h, (-dist, -point.x, -point.y))
                    heapq.heappop(h)
        ans = []
        while h:
            _, x, y = heapq.heappop(h)
            ans.append(Point(-x, -y))
        return ans[::-1]
    def getDistance(self, point, origin):
        return (point.x - origin.x) ** 2 + (point.y - origin.y) ** 2

```



