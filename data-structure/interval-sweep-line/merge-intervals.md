56. Merge Intervalss

Given a collection of intervals, merge all overlapping intervals.

For example,  
Given`[1,3],[2,6],[8,10],[15,18]`,  
return`[1,6],[8,10],[15,18]`.

Idea:

区间问题先排序起点：\
如果当前区间的终点小于等于上一个终点：当前区间已被涵盖，continue;\
如果当前区间的起点小于等于上一个终点：改变前一个区间的终点为当前区间终点;\
如果都不满足则把当前区间作为新的区间加入答案

Solution:
```py
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

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, Comparator.comparing((int[] interval) -> interval[0]));
        int start = intervals[0][0];
        int end = intervals[0][1];
        List<int[]> result = new ArrayList<int[]>();
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] > end) {
                result.add(new int[]{start, end});
                start = intervals[i][0];
            }
            end = Math.max(end, intervals[i][1]);
        }
        result.add(new int[]{start, end});

        return result.toArray(new int[result.size()][]);
    }
}
```
