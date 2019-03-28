Target Sum 解题报告

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols`+`and`-`. For each integer, you should choose one from`+`and`-`as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

**Example 1:**

```
Input:
 nums is [1, 1, 1, 1, 1], S is 3. 
Output:
 5
Explanation
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
There are 5 ways to assign symbols to make the sum of nums be target 3.
```

**Note:**

1. The length of the given array is positive and will not exceed 20.
2. The sum of elements in the given array will not exceed 1000.
3. Your output answer is guaranteed to be fitted in a 32-bit integer.

Idea:

这个题乍看上去就是Expression Add Operators的低配版：一次只能构造一个数，只有+和-没有乘。所以上来写一个DFS

```
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        # DFS
        self.nums = nums
        self.S = S
        self.ans = 0
        self.helper(0, 0)
        return self.ans
    def helper(self, pos, val):
        if pos == len(self.nums):
            if val == self.S:
                self.ans += 1
            return

        self.helper(pos + 1, val + self.nums[pos])
        self.helper(pos + 1, val - self.nums[pos])
```

然而并过不了，时间复杂度为O\(2^n\)过高了，那么就想到了DP。

仔细想想可以以sum为一个维度构造一个二维的f数组，也就是knapsack problem。

这个题目特殊的地方在于，可能构造出\[-sum, sum\]中的数，而数组的下标却只能是&gt;=的整数，所以要在数组下标和真正的value之间加入一个offset = sum

```
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        # DP: knapsack problem. 
        total = sum(nums)
        if abs(S) > total:
            return 0
        n = len(nums)
        f = [[0 for _ in xrange(2 * total + 1)] for _ in xrange(n + 1)]
        f[0][total] = 1
        for i in xrange(1, n + 1):
            for j in xrange(-total, total + 1, 1):
                if j - nums[i - 1] >= -total:
                    f[i][j + total] += f[i - 1][j - nums[i - 1] + total]
                if j + nums[i - 1] <= total:
                    f[i][j + total] += f[i - 1][j + nums[i - 1] + total]
        return f[n][S + total]
```

以上代码可以AC。但是还可以优化空间复杂度为O\(2\*sum\)

```
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        # DP: knapsack problem. 
        total = sum(nums)
        if abs(S) > total:
            return 0
        n = len(nums)
        f = [[0 for _ in xrange(2 * total + 1)] for _ in xrange(2)]
        f[0][total] = 1
        for i in xrange(1, n + 1):
            for j in xrange(-total, total + 1, 1):
                if j - nums[i - 1] >= -total and j + nums[i - 1] <= total:
                    f[i % 2][j + total] = f[(i - 1) % 2][j - nums[i - 1] + total] + \
                            f[(i - 1) % 2][j + nums[i - 1] + total]
                elif j + nums[i - 1] <= total:
                    f[i % 2][j + total] = f[(i - 1) % 2][j + nums[i - 1] + total]
                elif j - nums[i - 1] >= -total:
                    f[i % 2][j + total] = f[(i - 1) % 2][j - nums[i - 1] + total]
        return f[n % 2][S + total]
```



