High Five

There are two properties in the node student`id`and`scores`, to ensure that each student will have at least 5 points, find the average of 5 highest scores for each person.

**Example**

```
Given results = [[1,91],[1,92],[2,93],[2,99],[2,98],[2,97],[1,60],[1,58],[2,100],[1,61]]

Return 

```

思路：

这个题目比较简单的hash和heap的结合题目，是一个hashofheapq的题目。建立一个dict,key是id,存的是一个heapq,heapq里面设置一个size为5的最高5们课，如果size大于5则弹出最小值

```
'''
Definition for a Record
class Record:
    def __init__(self, id, score):
        self.id = id
        self.score = score
'''
from heapq import heappop, heappush
class Solution:
    # @param {Record[]} results a list of <student_id, score>
    # @return {dict(id, average)} find the average of 5 highest scores for each person
    # <key, value> (student_id, average_score)
    def highFive(self, results):
        # Write your code here
        hm = {}
        SIZE = 5
        for record in results:
            id, score = record.id, record.score
            if id not in hm:
                hm[id] = []
            heappush(hm[id], score)
            if len(hm[id]) > SIZE:
                heappop(hm[id])
        ans = {}
        for id in hm.keys():
            ans[id] = sum(hm[id]) / 5.0
        return ans
```

  
  


