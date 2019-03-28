Lintcode 447: Search in a Big Sorted Array 解题报告

Problem:

Given a big sorted array with positive integers sorted by ascending order. The array is so big so that you can not get the length of the whole array directly, and you can only access the kth number by`ArrayReader.get(k)`\(or ArrayReader-&gt;get\(k\) for C++\). Find the first index of a target number. Your algorithm should be in O\(log k\), where k is the first index of the target number.

Return -1, if the number doesn't exist in the array.

##### Notice

If you accessed an inaccessible index \(outside of the array\), ArrayReader.get will return`2,147,483,647`.

Example:

Given`[1, 3, 6, 9, 21, ...]`, and target =`3`, return`1`.

Given`[1, 3, 6, 9, 21, ...]`, and target =`4`, return`-1`.

Idea:

Need to find end first, with similar approach to binary search: 倍增法找end

Solution:

```
"""
Definition of ArrayReader:
class ArrayReader:
    def get(self, index):
        # this would return the number on the given index
        # return -1 if index is less than zero.
"""
class Solution:
    # @param {ArrayReader} reader: An instance of ArrayReader 
    # @param {int} target an integer
    # @return {int} an integer
    def searchBigSortedArray(self, reader, target):
        # write your code here
        start, end = 0, 1
        MAX_NUM = 1 << 31 - 1
        while reader.get(end) != MAX_NUM and reader.get(end) <= target:
            end *= 2
        while start + 1 < end:
            mid = (start + end) / 2
            if reader.get(mid) >= target:
                end = mid
            else:
                start = mid
        if reader.get(start) == target:
            return start
        if reader.get(end) == target:
            return end
        return -1
```



