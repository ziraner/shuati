Sliding Window Maximum解题报告

Given an arraynums, there is a sliding window of sizekwhich is moving from the very left of the array to the very right. You can only see theknumbers in the window. Each time the sliding window moves right by one position.

For example,  
Givennums=`[1,3,-1,-3,5,3,6,7]`, andk= 3.

```
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

Therefore, return the max sliding window as`[3,3,5,5,6,7]`.

**Note:**  
You may assumekis always valid, ie: 1 ≤ k ≤ input array's size for non-empty array.

Idea

这个题目需要用到deque来做，deque在python里面有自己的类        

from collections import deque  
append\(\)  
appendleft\(\)  
pop\(\)  
popleft\(\)

乍一看这个题其实bruteforce的话用hashmap保存window里面的数，然后删一个加一个，但是时间复杂度是O\(nk\)是不好的。想到了单调栈，然而发现需要从左边O\(1\)pop数，所以最后用deque，维护一个单调递减的deque

```
class Solution(object):
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        from collections import deque
        d = deque()
        ans = []
        for i in xrange(len(nums)):
            while d and d[-1] < nums[i]:
                d.pop()
            d.append(nums[i])
            if i >= k:
                if nums[i - k] == d[0]:
                    d.popleft()
            if i + 1 >= k:
                ans.append(d[0])
        return ans
```



