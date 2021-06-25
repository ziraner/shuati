Insert Interval 解题报告

Given a set of non-overlapping intervals, insert a new interval into the intervals \(merge if necessary\).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**  
Given intervals`[1,3],[6,9]`, insert and merge`[2,5]`in as`[1,5],[6,9]`.

**Example 2:**  
Given`[1,2],[3,5],[6,7],[8,10],[12,16]`, insert and merge`[4,9]`in as`[1,2],[3,10],[12,16]`.

This is because the new interval`[4,9]`overlaps with`[3,5],[6,7],[8,10]`.

Idea:

先找到插入点， 插入，在merge intervals

```py
class Solution(object):
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[Interval]
        :type newInterval: Interval
        :rtype: List[Interval]
        """
        idx, ans = 0, []
        while idx < len(intervals) and intervals[idx].start < newInterval.start:
            idx += 1
        intervals = intervals[:idx] + [newInterval] + intervals[idx:]
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
    public int[][] insert(int[][] intervals, int[] newInterval) {
        if (newInterval == null || newInterval.length == 0) {
            return intervals;
        }
        // insert
        int[][] newIntervals = new int[intervals.length + 1][2];
        int idx = 0;
        while (idx < intervals.length && intervals[idx][0] < newInterval[0]) {
            newIntervals[idx] = intervals[idx];
            idx++;
        }
        newIntervals[idx] = newInterval;
        idx++;
        while (idx < intervals.length + 1) {
            newIntervals[idx] = intervals[idx - 1];
            idx++;
        }

        // merge
        List<int[]> results = new LinkedList<int[]>();
        for (int[] interval: newIntervals) {
            if (!results.isEmpty() && interval[1] <= results.get(results.size() - 1)[1]) {
                continue;
            }
            if (!results.isEmpty() && interval[0] <= results.get(results.size() - 1)[1]) {
                results.get(results.size() - 1)[1] = interval[1];
                continue;
            }
            results.add(interval);
        }
        return results.toArray(new int[results.size()][]);
    }
}
```
