Backpack IV 解题报告

Given n items with size`nums[i]`which an integer array and all positive numbers, no duplicates. An integer`target`denotes the size of a backpack. Find the number of possible fill the backpack.

`Each item may be chosen unlimited number of times`

**Example**

Given candidate items`[2,3,6,7]`and target`7`,

```
A solution set is: 
[7]
[2, 2, 3]
```

无限背包问题

f\[i\]\[S\] “前i”个物品，取出一些能否组成和为S

f\[i\]\[S\] = f\[i-1\]\[S - k\*a\[i-1\]\] or f\[i-1\]\[S\]     a\[i-1\] 是第i个物品下标是i-1            k 是第i个物品选取的次数

下述解法的时间复杂度是O\(n\*S\*S\)过于高了

```
class Solution:
    """
    @param: nums: an integer array and all positive numbers, no duplicates
    @param: target: An integer
    @return: An integer
    """
    def backPackIV(self, nums, target):
        # write your code here
        if not nums:
            return 0
        n = len(nums)
        # method from class: with k
        """
        f = [[0 for _ in xrange(target + 1)] for _ in xrange(2)]
        f[0][0] = 1
        for i in xrange(1, n + 1):
            f[i % 2][0] = 1
            for j in xrange(1, target + 1):
                f[i % 2][j] = f[(i - 1) % 2][j]
                k = 1
                while j >= k * nums[i - 1]:
                    f[i % 2][j] += f[(i - 1) % 2][j - k * nums[i - 1]]
                    k += 1
        return f[n % 2][target]
```

利用完全背包问题时间复杂度的改善去掉k循环

f\[i\]\[S\] = f\[i\]\[S - k\*a\[i-1\]\] or f\[i\]\[S\]

```
class Solution:
    """
    @param: nums: an integer array and all positive numbers, no duplicates
    @param: target: An integer
    @return: An integer
    """
    def backPackIV(self, nums, target):       
        # method from BackPack III
        f = [[0 for _ in xrange(target + 1)] for _ in xrange(2)]
        f[0][0] = 1
        for i in xrange(1, n + 1):
            f[i % 2][0] = 1
            for j in xrange(1, target + 1):
                f[i % 2][j] = f[(i - 1) % 2][j]
                if j >= nums[i - 1]:
                    f[i % 2][j] += f[i % 2][j - nums[i - 1]]
        return f[n % 2][target]
```



