Merge Intervals 解题报告

Given a collection of intervals, merge all overlapping intervals.

For example,  
Given`[1,3],[2,6],[8,10],[15,18]`,  
return`[1,6],[8,10],[15,18]`.

Idea:

区间问题先排序起点：

如果当前区间的终点小于等于上一个终点：当前区间已被涵盖，continue

如果当前区间的起点小于等于上一个终点：改变前一个区间的终点为当前区间终点

如果都不满足则把当前区间作为新的区间加入答案

```
class Solution(object):
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        if not intervals:
            return []
        intervals.sort(key = lambda x: x.start)
        ans = []
        for interval in intervals:
            if ans and ans[-1].end >= interval.end:
                continue
            if ans and ans[-1].end >= interval.start:
                ans[-1].end = interval.end
                continue
            ans.append(interval)
        return ans
```



