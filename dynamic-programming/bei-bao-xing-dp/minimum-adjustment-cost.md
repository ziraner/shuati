Minimum Adjustment Cost 解题报告

Given an integer array, adjust each integers so that the difference of every adjacent integers are not greater than a given number target.

If the array before adjustment is**A**, the array after adjustment is**B**, you should minimize the sum of`|A[i]-B[i]|`

##### Notice

You can assume each number in the array is a positive integer and not greater than`100`.

**Example**

Given`[1,4,2,3]`and target =`1`, one of the solutions is`[2,3,2,3]`, the adjustment cost is`2`and it's minimal.

思路： 

f\[i\]\[v\] 前i个数，第i个数调整为v，满足相邻两数&lt;= target的最小代价

f\[i\]\[v\] = min\(f\[i-1\]\[v’\] + \|A\[i\]-v\|, \|v-v’\|

f\[n\]\[a\[n\]-target~a\[n\]+target\]

```
from sys import maxint
class Solution:
    """
    @param: A: An integer array
    @param: target: An integer
    @return: An integer
    """
    def MinAdjustmentCost(self, A, target):
        # write your code here
        # f[i][j]: qian i ge shu, i bian wei j, man zu ti yi, zui xiao dai jia
        n = len(A)
        MAX_NO = 100
        f = [[maxint for _ in xrange(MAX_NO + 1)] for _ in xrange(n + 1)]
        for j in xrange(MAX_NO + 1):
            f[0][j] = 0
        for i in xrange(1, n + 1):
            # j is value in index i - 1
            for j in xrange(MAX_NO + 1):
                # if f[i - 1][j] is maxint no need to calculate
                if f[i - 1][j] == maxint:
                    continue
                # k is changed value in index i
                for k in xrange(MAX_NO + 1):
                    if abs(j - k) <= target:
                        f[i][k] = min(f[i][k], f[i - 1][j] + abs(k - A[i - 1]))
        return min(f[n])
```



