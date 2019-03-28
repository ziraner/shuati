Trapping Rain Water解题报告

Given\_n\_non-negative integers representing an elevation map where the width of each bar is`1`, compute how much water it is able to trap after raining.

![](https://lintcode-media.s3.amazonaws.com/problem/rainwatertrap.png "Trapping Rain Water")

**Example**

Given`[0,1,0,2,1,0,1,3,2,1,2,1]`, return`6`.

Idea

方法一：用两个数组保存从该点向左看向右看看到的最高高度是多少left\[\], right\[\]

```
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        # O(n) space
        n = len(height)
        if n <= 2:
            return 0
        left = [0 for _ in xrange(n + 1)]
        right = [0 for _ in xrange(n + 1)]
        for i in xrange(1, n + 1):
            left[i] = max(left[i - 1], height[i - 1])
        for i in xrange(n - 1, 0, -1):
            right[i] = max(right[i + 1], height[i])
        ans = 0
        for i in xrange(1, n - 1):
            bound = min(left[i], right[i])
            if bound > height[i]:
                ans += bound - height[i]
        return ans
```

方法二：两根指针，另用两个变量保存左边和右边最高的边是什么

```
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        #O(1) space
        n = len(height)
        if n <= 2:
            return 0
        left, right = 0, n - 1
        leftHeight, rightHeight = height[left], height[right]
        ans = 0
        while left < right:
            if leftHeight < rightHeight:
                left += 1
                if height[left] < leftHeight:
                    ans += leftHeight - height[left]
                else:
                    leftHeight = height[left]
            else:
                right -= 1
                if height[right] < rightHeight:
                    ans += rightHeight - height[right]
                else:
                    rightHeight = height[right]
        return ans
```



