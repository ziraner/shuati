Burst Balloons解题报告

Given`n`balloons, indexed from`0`to`n-1`. Each balloon is painted with a number on it represented by array`nums`. You are asked to burst all the balloons. If the you burst balloon`i`you will get`nums[left] * nums[i] * nums[right]`coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the`maximum`coins you can collect by bursting the balloons wisely.

* You may imagine`nums[-1] = nums[n] = 1`. They are not real therefore you can not burst them.  
* 0 ≤`n`≤ 500, 0 ≤`nums[i]`≤ 100

**Example**

Given`[4, 1, 5, 10]`  
Return`270`

```
nums = [4, 1, 5, 10] burst 1, get coins 4 * 1 * 5 = 20
nums = [4, 5, 10]    burst 5, get coins 4 * 5 * 10 = 200 
nums = [4, 10]       burst 4, get coins 1 * 4 * 10 = 40
nums = [10]          burst 10, get coins 1 * 10 * 1 = 10

Total coins 20 + 200 + 40 + 10 = 270
```

区间型DP

state：dp\[i\]\[j\] 表示把第i到第j个气球打爆的最大价值

Function:

• 对于所有k属于{i,j}, 表示第k号气球最后打爆。

• midValue = arr\[i-1\] \* arr\[k\] \* arr\[j+1\] 最后一个打爆k的得分

• dp\[i\]\[j\] = max\(dp\[i\]\[k-1\]+dp\[k+1\]\[j\]+midvalue\)

Initialization：

for each i

• dp\[i\]\[i\] = arr\[i-1\] \* arr\[i\] \* arr\[i+1\];

```
class Solution(object):
    def maxCoins(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        n = len(nums)
        nums = [1] + nums + [1]
        dp = [[0 for _ in xrange(n + 2)] for _ in xrange(n + 2)]
        flag = [[False for _ in xrange(n + 2)] for _ in xrange(n + 2)]
        return self.msearch(dp, flag, nums, 1, n)
    def msearch(self, dp, flag, nums, x, y):
        if flag[x][y]:
            return dp[x][y]
        flag[x][y] = True
        for i in xrange(x, y + 1):
            left = self.msearch(dp, flag, nums, x, i - 1)
            right = self.msearch(dp, flag, nums, i + 1, y)
            dp[x][y] = max(left + right + nums[i] * nums[x - 1] * nums[y + 1], dp[x][y])
        return dp[x][y]
```



