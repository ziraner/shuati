Largest Rectangle in Histogram 解题报告

Given\_n\_non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](https://lintcode-media.s3.amazonaws.com/problem/histogram1.png "histogram")

Above is a histogram where width of each bar is 1, given height =`[2,1,5,6,2,3]`.

![](https://lintcode-media.s3.amazonaws.com/problem/histogram_area.png "histogram")

The largest rectangle is shown in the shaded area, which has area =`10`unit.

**Example**

Given height = `[2,1,5,6,2,3]`,  
return `10`.

Idea:

单调增栈，栈中保存idx

在栈pop的操作中计算height = nums\[stack.pop\(\)\] 计算width = stack为空当前元素的idx；stack不为空当前元素的idx - stack\[-1\] - 1

```
class Solution(object):
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        if not heights:
            return 0
        stack = []
        ans = 0
        heights.append(-1)
        for i in xrange(len(heights)):
            while stack and heights[stack[-1]] > heights[i]:
                h = heights[stack.pop()]
                if stack:
                    w = i - stack[-1] - 1
                else:
                    w = i
                ans = max(ans, w * h)
            stack.append(i)
        return ans
```



