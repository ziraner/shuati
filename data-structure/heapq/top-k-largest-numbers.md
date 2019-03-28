Top k Largest Numbers 解题报告

Given an integer array, find the top\_k\_largest numbers in it.

**Example**

Given`[3,10,1000,-99,4,100]`and_k_=`3`.  
Return`[1000, 100, 10]`.

Idea:

方法一：heapsort，直接用heapq里面的heapify和nlargest函数

```
import heapq

class Solution:
    '''
    @param {int[]} nums an integer array
    @param {int} k an integer
    @return {int[]} the top k largest numbers in array
    '''
    def topk(self, nums, k):
        # Write your code here
        # mimic java priority queue solution
        """
        heapq.heapify(nums)
        return heapq.nlargest(k, nums)
```

方法二：手动实现heapsort

```
import heapq

class Solution:
    '''
    @param {int[]} nums an integer array
    @param {int} k an integer
    @return {int[]} the top k largest numbers in array
    '''
    def topk(self, nums, k):
        # Write your code here
        # mimic java priority queue solution
        import sys
        h = [-sys.maxint]
        result = []
        for num in nums:
            if len(h) < k:
                heapq.heappush(h, num)
            else:
                if h[0] > num:
                    continue
                heapq.heappush(h, num)
                heapq.heappop(h)
        for i in range(k):
            result.append(heapq.heappop(h))
        return result[::-1]
```

方法三：quicksort直到start &gt;= k:

```
class Solution:
    '''
    @param {int[]} nums an integer array
    @param {int} k an integer
    @return {int[]} the top k largest numbers in array
    '''
    def topk(self, nums, k):
        # quicksort until start >= k
        """
        self.quickSort(nums, 0, len(nums) - 1, k)
        return nums[:k]
    def quickSort(self, nums, start, end, k):
        if start >= end:
            return
        if start >= k:
            return
        left, right = start, end
        pivot = nums[(start + end) / 2]
        while left <= right:
            while left <= right and nums[left] > pivot:
                left += 1
            while left <= right and nums[right] < pivot:
                right -= 1
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        self.quickSort(nums, start, right, k)
        self.quickSort(nums, left, end, k)
```



