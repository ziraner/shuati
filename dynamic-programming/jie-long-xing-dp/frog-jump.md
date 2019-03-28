Frog Jump解题报告

A frog is crossing a river. The river is divided into x units and at each unit there may or may not exist a stone. The frog can jump on a stone, but it must not jump into the water.

Given a list of stones' positions \(in units\) in sorted ascending order, determine if the frog is able to cross the river by landing on the last stone. Initially, the frog is on the first stone and assume the first jump must be 1 unit.

If the frog's last jump was k units, then its next jump must be either`k - 1`,`k`, or`k + 1`units. Note that the frog can only jump in the forward direction.

##### Notice

* The number of stones is ≥ `2`and is &lt;`1100`.
* Each stone's position will be a non-negative integer &lt;`2^31`.
* The first stone's position is always`0.`

Idea:

这个题的状态方程很难因为青蛙不一定需要每一块儿石头都落。  
\[0,1,3,5,6,8,12,17\] it jumps from 5 -&gt; 8 cannot jump from 6 -&gt; 8 因为从6到8是不够的。  
所以我们建立一个f是一个hashmap来存假设青蛙可以跳跃到当前石头，那么它所用的所有可能的jump是什么（存成set的形式）

那么初始化就是f\[0\] = set\(\[0\]\)我们扫所有的stone，对f\[stone\]中所有的jump讨论，jump - 1, jump, jump + 1可以跳到哪些时候上，且将它们保存在对应石头的set中。

```
class Solution(object):
    def canCross(self, stones):
        """
        :type stones: List[int]
        :rtype: bool
        """
        f = {}
        for stone in stones:
            f[stone] = set([])
        f[0].add(0)
        for stone in stones:
            for jump in f[stone]:
                if jump > 1 and jump - 1 + stone in f:
                    f[jump - 1 + stone].add(jump - 1)
                if jump + stone in f:
                    f[jump + stone].add(jump)
                if jump + 1 + stone in f:
                    f[jump + stone + 1].add(jump + 1)
        return len(f[stones[-1]]) != 0
```

  




