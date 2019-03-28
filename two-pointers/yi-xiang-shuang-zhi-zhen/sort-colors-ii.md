Sort Colors II 解题报告

Given an array of _n _objects with _k _different colors \(numbered from 1 to k\), sort them so that objects of the same color are adjacent, with the colors in the order 1, 2, ... k.

Notice

You are not suppose to use the library's sort function for this problem.

k &lt;= n

**Example**

Given colors=`[3, 2, 2, 1, 4]`,`k=4`, your code should sort colors in-place to`[1, 2, 2, 3, 4]`.

Idea:

和quicksort类似，不同点在于

1.怎么处理==pivot的数，这个题目中，==pivot的只能在左边不能在右边。

2.另外加了一个sort的上下限，可以降低时间复杂度Nlogk

```
class Solution:
    """
    @param colors: A list of integer
    @param k: An integer
    @return: nothing
    """
    def sortColors2(self, colors, k):
        # write your code here
        self.helper(colors, 1, k, 0, len(colors) - 1)
    def helper(self, colors, colorFrom, colorTo, start, end):
        if start >= end:
            return
        if colorFrom == colorTo:
            return
        left, right = start, end
        pivot = (colorFrom + colorTo) / 2
        while left <= right:
            while left <= right and colors[left] <= pivot:
                left += 1
            while left <= right and colors[right] > pivot:
                right -= 1
            if left <= right:
                colors[left], colors[right] = colors[right], colors[left]
                left += 1
                right -= 1
        self.helper(colors, colorFrom, pivot, start, right)
        self.helper(colors, pivot + 1, colorTo, left, end)
```



  
  
  


