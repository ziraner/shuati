Jump Game 解题报告

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

##### Notice

This problem have two method which is`Greedy`and`Dynamic Programming`.

The time complexity of`Greedy`method is`O(n)`.

The time complexity of`Dynamic`Programming method is`O(n^2)`.

We manually set the small data set to allow you pass the test in both ways. This is just to let you learn how to use this problem in dynamic programming ways. If you finish it in dynamic programming ways, you can try greedy method to make it accept again.

**Example**

A =`[2,3,1,1,4]`, return`true`.

A =`[3,2,1,0,4]`, return`false`.

思路：

DP

function f\[i\] = for all j &lt; i OR\(f\[j\] && j + A\[j\] &gt;= i\)

```
class Solution:
    """
    @param: A: A list of integers
    @return: A boolean
    """
    def canJump(self, A):
        # write your code here
        if A is None:
            return True
        n = len(A)
        # f[i] means whether index i can be reached or not
        f = [False for _ in range(n)]
        f[0] = True
        # 
        for i in range(1, n):
            for j in range(0, i):
                if not f[j]:
                    continue
                if A[j] + j >= i:
                    f[i] = True
                    break
        return f[n - 1]
```



