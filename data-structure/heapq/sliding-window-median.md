Sliding Window Median解题报告

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples:

`[2,3,4]`, the median is`3`

`[2,3]`, the median is`(2 + 3) / 2 = 2.5`

Given an arraynums, there is a sliding window of sizekwhich is moving from the very left of the array to the very right. You can only see theknumbers in the window. Each time the sliding window moves right by one position. Your job is to output the median array for each window in the original array.

For example,  
Givennums=`[1,3,-1,-3,5,3,6,7]`, andk= 3.

```
Window position                Median
---------------               -----
[1  3  -1] -3  5  3  6  7       1
 1 [3  -1  -3] 5  3  6  7       -1
 1  3 [-1  -3  5] 3  6  7       -1
 1  3  -1 [-3  5  3] 6  7       3
 1  3  -1  -3 [5  3  6] 7       5
 1  3  -1  -3  5 [3  6  7]      6
```

Therefore, return the median sliding window as`[1,-1,-1,3,5,6]`.

LeetCode这个题目稍微复杂点需要判断是奇是偶，所以就以这个题目为类做。

这个题目要用到hashheap因为要支持O\(logn\)的删除。HashHeap的代码不include进来了去hashheap题目里找

这个题目类似是find median from data stream的加强版，也需要用一个最大堆一个最小堆去维护。

在添加/删除node的时候，我们需要把到了k和没到k分情况讨论，因为adjust的时候最多调整一次，所以要把push的地方分摊在两个地方写，因为如果不管条件直接先push进去的话，再讨论删除，是不对的。

```
class Solution(object):
    def medianSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[float]
        """
        minHeap, maxHeap = HashHeap(), HashHeap()
        ans = []
        for i in xrange(len(nums)):
            if i < k:
                if i % 2 == 0:
                    maxHeap.push(-nums[i])
                else:
                    minHeap.push(nums[i])
            else:
                if -maxHeap.top() < nums[i - k]:
                    minHeap.remove(nums[i - k])
                    minHeap.push(nums[i])
                else:
                    maxHeap.remove(-nums[i - k])
                    maxHeap.push(-nums[i])
            if not minHeap.isEmpty() and -maxHeap.top() > minHeap.top():
                sm, lg = minHeap.pop(), -maxHeap.pop()
                minHeap.push(lg)
                maxHeap.push(-sm)
            if i + 1 >= k:
                median = 0
                if k % 2 == 0:
                    median = (minHeap.top() - maxHeap.top()) / 2.0
                else:
                    median = -maxHeap.top() / 1.0
                ans.append(median)
        return ans
```



