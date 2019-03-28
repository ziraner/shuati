Building Outline\(LintCode\) The Skyline Problem\(LeetCode\) 解题报告

Given\_N\_buildings in a x-axis，each building is a rectangle and can be represented by a triple \(start, end, height\)，where start is the start position on x-axis, end is the end position on x-axis and height is the height of the building. Buildings may overlap if you see them from far away，find the outline of them。

An outline can be represented by a triple, \(start, end, height\), where start is the start position on x-axis of the outline, end is the end position on x-axis and height is the height of the outline.

![](https://lintcode-media.s3.amazonaws.com/problem/jiuzhang3.jpg "Building Outline")

##### Notice

Please merge the adjacent outlines if they have the same height and make sure different outlines cant overlap on x-axis.

**Example**

Given 3 buildings：

```
[
  [1, 3, 3],
  [2, 4, 4],
  [5, 6, 1]
]
```

The outlines are：

```
[
  [1, 2, 3],
  [2, 4, 4],
  [5, 6, 1]
]
```

LeetCode: 返回：

For instance, the skyline in Figure B should be represented as:`[ [2 10], [3 15], [7 12], [12 0], [15 10], [20 8], [24, 0] ]`.

LeetCode代码（不包括hashheap，hashheap代码在[这儿](/heapq/hashheap.md)）

这个题目需要按照扫描线的思路，将起点，终点分开来，建在一个三维的tuple里面，起点赋值-1，终点赋值1。然后对这些tuple进行排序，则起点会排序在终点前面，如果终点排序在起点前面的话是有问题的：  
\#\[\[0, 2, 3\], \[2, 5, 3\]\] otherwise the result will be \[\[0, 3\], \[2, 3\], \[5, 0\]\]

然后建立一个hashheap，之所以要hashheap是因为要支持O\(logn\)的删除。维护hashheap的同时维护一个hashmap存当前点输出的值。遇到起点

```
class Solution(object):
    def getSkyline(self, buildings):
        """
        :type buildings: List[List[int]]
        :rtype: List[List[int]]
        """
        edges = []
        for x, y, h in buildings:
            edges.append((x, h, -1))
            edges.append((y, h, 1))
        # sort from start to end cannot from end to start
        #[[0, 2, 3], [2, 5, 3]] otherwise the result will be [[0, 3], [2, 3], [5, 0]]
        edges.sort()
        maxHeap, hm = HashHeap(), {}
        for i, h, status in edges:
            if status == -1:
                if maxHeap.isEmpty() or -maxHeap.top() < h:
                    hm[i] = h
                maxHeap.push(-h)
            else:
                maxHeap.remove(-h)
                if maxHeap.isEmpty():
                    hm[i] = 0
                elif -maxHeap.top() < h:
                    hm[i] = -maxHeap.top()
        ans = []
        for key in sorted(hm.keys()):
            ans.append([key, hm[key]])
        return ans
```



