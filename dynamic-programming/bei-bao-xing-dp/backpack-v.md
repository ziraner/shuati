Backpack V 解题报告

Given n items with size`nums[i]`which an integer array and all positive numbers. An integer`target`denotes the size of a backpack. Find the number of possible fill the backpack.

`Each item may only be used once`

**Example**

Given candidate items`[1,2,3,3,7]`and target`7`,

```
A solution set is: 
[7]
[1, 3, 3]

```

return`2`

背包DP，滚动数组优化方法，然而过不了AC

```
class Solution:
    """
    @param: nums: an integer array and all positive numbers
    @param: target: An integer
    @return: An integer
    """
    def backPackV(self, nums, target):
        # write your code here
        # a 01 BackPack of NB version BackPack IV
        # O(2n) space guo bu liao
        n = len(nums)
        f = [[0 for _ in xrange(target + 1)] for _ in xrange(2)]
        f[0][0] = 1
        for i in xrange(1, n + 1):
            f[i % 2][0] = 1
            for j in xrange(1, target + 1):
                f[i % 2][j] = f[(i - 1) % 2][j]
                if j >= nums[i - 1]:
                    f[i % 2][j] += f[(i - 1) % 2][j - nums[i - 1]]
        return f[n % 2][target]
```

改进以后，只有一个数组，可以过AC，需要注意的是j的循环需要从大向小循环因为其实是

f\[i\]\[j\] = f\[i - 1\]\[j - nums\[i - 1\]\]，我们需要利用上一层的i - 1的较小值去calculate j，所以为了不overwrite，必须从大向小循环。

不得不吐槽一句为了改进空间复杂度从O\(2n\)到O\(n\)也真他妈够复杂的了。

```
class Solution:
    """
    @param: nums: an integer array and all positive numbers
    @param: target: An integer
    @return: An integer
    """
    def backPackV(self, nums, target):
        # write your code here
        # O(n) space, j from back to front: not overwrite f[i -1][j - nums[i - 1]]
        # f[i][j] = f[i - 1][j](current f[i][j]) + f[i - 1][j - nums[i - 1]] 
        n = len(nums)
        f = [0 for _ in xrange(target + 1)]
        f[0] = 1
        for i in xrange(1, n + 1):
            for j in xrange(target, 0, -1):
                if j >= nums[i - 1]:
                    f[j] += f[j - nums[i - 1]]
        return f[target]
```



