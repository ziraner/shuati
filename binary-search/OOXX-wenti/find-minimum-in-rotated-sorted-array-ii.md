Lintcode 160: Find Minimum in Rotated Sorted Array II 解题报告

Problem:

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

\(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2\).

Find the minimum element.

##### Notice

The array may contain duplicates.

Example

Given`[4,4,5,6,7,0,1,2]`return`0`.

Idea:

必须得从头扫一遍，不能用二分， 反例：\[1, 1, 1, 1, 0, 1,1, 1, 1, 1\]

Solution:

```
class Solution:
    # @param num: a rotated sorted array
    # @return: the minimum number in the array
    def findMin(self, num):
        # write your code here
        return min(num)
```



