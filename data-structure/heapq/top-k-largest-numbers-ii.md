Top k Largest Numbers II 解题报告

Implement a data structure, provide two interfaces:

1. `add(number)`. Add a new number in the data structure.
2. `topk()`. Return the top _k _largest numbers in this data structure. _k _is given when we create the data structure.

```
import heapq
class Solution:
    # @param {int} k an integer
    def __init__(self, k):
        # initialize your data structure here.
        self.h = []
        self.capacity = k
    # @param {int} num an integer
    def add(self, num):
        # Write your code here
        if self.capacity > len(self.h):
            heapq.heappush(self.h, num)
        else:
            if self.h[0] > num:
                return
            heapq.heappop(self.h)
            heapq.heappush(self.h, num)
    # @return {int[]} the top k largest numbers
    def topk(self):
        # Write your code here
        # use nlargest from python heapq
        """
        l = heapq.nlargest(self.capacity, self.h)
        return l
        """
        # cannot use nlargest from python heapq
        l = []
        tmp = self.h[:]
        for i in range(len(self.h)):
            l.append(heapq.heappop(tmp))
        return l[::-1]
```



