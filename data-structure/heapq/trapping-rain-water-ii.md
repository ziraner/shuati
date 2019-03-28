Trapping Rain Water II 解题报告

Given_n\_x\_m\_non-negative integers representing an elevation map 2d where the area of each cell is\_1\_x\_1_, compute how much water it is able to trap after raining.

![](https://lintcode-media.s3.amazonaws.com/problem/trapping-rain-water-ii.jpg)

**Example**

Given`5*4`matrix

```
[12,13,0,12]
[13,4,13,12]
[13,8,10,12]
[12,13,12,12]
[13,13,13,13]
```

return`14`.

Idea:

把最外圈的\(height, x, y\)加进minheap中，然后向内做BFS遍历。每次弹出minheap中最小的元素，然后四个方向遍历，如果遇到比当前height还小的height更新ans，然后将较高的heightl和xx, yy 继续放进heap中，同时需要一个visited数组记录遍历过哪些点。  
需要注意cornercase就是初始将四个角落的点放进heap，因为循环的关系可能会重复，但是没关系四个角BFS的时候哪儿都去不了；但是一定要将它们放进minheap否则它们会被遍历，会被当做可以装雨水的点进行计算。

```
class Solution(object):
    def trapRainWater(self, heightMap):
        """
        :type heightMap: List[List[int]]
        :rtype: int
        """
        h = []
        if not heightMap or not heightMap[0]:
            return 0
        m, n = len(heightMap), len(heightMap[0])
        visited = [[False for _ in xrange(n)] for _ in xrange(m)]
        ans, h = 0, []
        from heapq import heappush, heappop
        for i in xrange(m):
            heappush(h, (heightMap[i][0], i, 0))
            visited[i][0] = True
            heappush(h, (heightMap[i][n - 1], i, n - 1))
            visited[i][n - 1] = True
        for j in xrange(n):
            heappush(h, (heightMap[0][j], 0, j))
            visited[0][j] = True
            heappush(h, (heightMap[m - 1][j], m - 1, j))
            visited[m - 1][j] = True
        while h:
            height, x, y = heappop(h)
            for deltax, deltay in [[1, 0], [-1, 0], [0, 1], [0, -1]]:
                xx, yy = x + deltax, y + deltay
                if xx < m and xx >= 0 and yy < n and yy >= 0 and not visited[xx][yy]:
                    heappush(h, (max(heightMap[xx][yy], height), xx, yy))
                    visited[xx][yy] = True
                    if heightMap[xx][yy] < height:
                        ans += height - heightMap[xx][yy]
        return ans
```



