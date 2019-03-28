Kth Largest Element II 解题报告

Find K-th largest element in an array. and N is much larger than k.

##### Notice

You can swap elements in the array

**Example**

In array`[9,3,2,4,8]`, the`3rd`largest element is`4`.

In array`[1,2,3,4,5]`, the`1st`largest element is`5`,`2nd`largest element is`4`,`3rd`largest element is`3`and etc.

Idea:

这个题最好的解决方案还是quickselect，II比I多了一个条件就是N要远大于k则Nlogk可以约等于N，所以用heap也可以

```
from heapq import heappush, heappop
class Solution:
    # @param nums {int[]} an integer unsorted array
    # @param k {int} an integer from 1 to n
    # @return {int} the kth largest element
    def kthLargestElement2(self, nums, k):
        # Write your code here
        # heapq
        hpq = []
        for num in nums:
            if k > len(hpq):
                heappush(hpq, num)
            else:
                if num > hpq[0]:
                    heappush(hpq, num)
                    heappop(hpq)
        return hpq[0]
```



