meeting rooms II 解题报告

Given an array of meeting time intervals consisting of start and end times`[[s1,e1],[s2,e2],...]`\(si&lt; ei\), find the minimum number of conference rooms required.

For example,  
Given`[[0, 30],[5, 10],[15, 20]]`,  
return`2`.

Idea:

解法1：跟数飞机一样，用扫描线解

```
class Solution(object):
    def minMeetingRooms(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: int
        """
        if not intervals:
            return 0
        t = []
        for interval in intervals:
            t.append([interval.start, 1])
            t.append([interval.end, -1])
        t.sort(key = lambda x: (x[0], x[1]))
        cnt, ans = 0, 0
        for _, status in t:
            cnt += status
            ans = max(cnt, ans)
        return ans
```

解法2：跟general interval题目一样，先按照起点排序；维护一个minheap保存end， 如果下一个start &gt;= 最小的end，则pop。最后返回heap的长度即为所求

```
class Solution(object):
    def minMeetingRooms(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: int
        """
        if not intervals:
            return 0
        intervals.sort(key = lambda x: x.start)
        hq = []
        from heapq import heappush, heappop
        for interval in intervals:
            if hq and hq[0] <= interval.start:
                heappop(hq)
            heappush(hq, interval.end)
        return len(hq)
```



