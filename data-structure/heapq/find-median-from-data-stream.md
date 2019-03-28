Find Median from Data Stream\(leetcode\)/Data Stream Median\(Lintcode\) 解题报告

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples:

`[2,3,4]`, the median is`3`

`[2,3]`, the median is`(2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:

* void addNum\(int num\) - Add a integer number from the data stream to the data structure.
* double findMedian\(\) - Return the median of all elements so far.

For example:

```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

leetcode这个题是让我们设计一个数据结构，然后这个数据结构有addNum和findMedian两个操作。median操作如果是even的话要平均。

而lintcode这个题是有一个数组，这个数组上的值源源不断的加入，求另外一个数组，那个数组保存的是进来这些值到当前idx的median。even的话不需要平均，取小的那个。时间复杂度O\(nlogn\)

Lintcode题目的代码

```
from heapq import heappush, heappop
class Solution:
    """
    @param: nums: A list of integers
    @return: the median of numbers
    """
    def medianII(self, nums):
        # write your code here
        # number > median
        minheap = []
        # number <= median
        maxheap = []
        ans = []
        for i in range(len(nums)):
            # add first
            if i % 2 == 0:
                heappush(maxheap, -nums[i])
            else:
                heappush(minheap, nums[i])
            # adjust second
            if len(minheap) != 0 and -maxheap[0] > minheap[0]:
                tmp1 = -heappop(maxheap)
                tmp2 = heappop(minheap)
                heappush(maxheap, -tmp2)
                heappush(minheap, tmp1)
            ans.append(-maxheap[0])
        return ans
```

LeetCode的代码

```
from heapq import heappush, heappop
class MedianFinder(object):

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.minHeap = []
        self.maxHeap = []
        self.size = 0

    def addNum(self, num):
        """
        :type num: int
        :rtype: void
        """
        if self.size % 2 == 0:
            heappush(self.maxHeap, -num)
        else:
            heappush(self.minHeap, num)
        
        if self.minHeap and -self.maxHeap[0] > self.minHeap[0]:
            lg, sm = -heappop(self.maxHeap), heappop(self.minHeap)
            heappush(self.maxHeap, -sm)
            heappush(self.minHeap, lg)
        self.size += 1

    def findMedian(self):
        """
        :rtype: float
        """
        if self.size == 0:
            return 0
        if self.size % 2 != 0:
            return -self.maxHeap[0]
        return (-self.maxHeap[0] + self.minHeap[0]) / 2.0


# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```



