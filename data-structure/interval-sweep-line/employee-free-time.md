759. Employee Free Time

We are given a list schedule of employees, which represents the working time for each employee.

Each employee has a list of non-overlapping Intervals, and these intervals are in sorted order.

Return the list of finite intervals representing common, positive-length free time for all employees, also in sorted order.

(Even though we are representing Intervals in the form [x, y], the objects inside are Intervals, not lists or arrays. For example, schedule[0][0].start = 1, schedule[0][0].end = 2, and schedule[0][0][0] is not defined).  Also, we wouldn't include intervals like [5, 5] in our answer, as they have zero length.



Example 1:
```
Input: schedule = [[[1,2],[5,6]],[[1,3]],[[4,10]]]
Output: [[3,4]]
Explanation: There are a total of three employees, and all common
free time intervals would be [-inf, 1], [3, 4], [10, inf].
We discard any intervals that contain inf as they aren't finite.
```
Example 2:
```
Input: schedule = [[[1,3],[6,7]],[[2,4]],[[2,5],[9,12]]]
Output: [[5,6],[7,9]]
```

Constraints:
```
1 <= schedule.length , schedule[i].length <= 50
0 <= schedule[i].start < schedule[i].end <= 10^8
```

解题思路：
interval sweepline问题，对所有interval按照起点、终点进行排序，然后两两interval比较。用一个全局变量记录maxEnd，如果interval的start小于maxEnd那么[maxEnd, start]构成一个free time，然后更新maxEnd

Solution
```java
class Solution {
    public List<Interval> employeeFreeTime(List<List<Interval>> schedule) {
        List<Interval> allIntervals = new ArrayList<>();
        for (List<Interval> intervals: schedule) {
            for (Interval interval: intervals) {
                allIntervals.add(interval);
            }
        }

        allIntervals.sort(Comparator.comparing((Interval interval) -> interval.start).thenComparing((Interval interval) -> interval.end));

        List<Interval> result = new ArrayList<>();
        int end = allIntervals.get(0).end;
        for (Interval interval: allIntervals) {
            if (interval.start > end) {
                result.add(new Interval(end, interval.start));
            }
            end = Math.max(end, interval.end);
        }
        return result;
    }
}
```
