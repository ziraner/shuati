Count Different Palindromic Subsequences 解题报告

Given a string S, find the number of different non-empty palindromic subsequences in S, and**return that number modulo**`10^9 + 7`**.**

A subsequence of a string S is obtained by deleting 0 or more characters from S.

A sequence is palindromic if it is equal to the sequence reversed.

Two sequences`A_1, A_2, ...`and`B_1, B_2, ...`are different if there is some`i`for which`A_i != B_i`.

**Example 1:**

```
Input: S = 'bccb'

Output: 6

Explanation:
The 6 different non-empty palindromic subsequences are 'b', 'c', 'bb', 'cc', 'bcb', 'bccb'.
Note that 'bcb' is counted only once, even though it occurs twice.
```

**Example 2:**

```
Input: S = 'abcdabcdabcdabcdabcdabcdabcdabcddcbadcbadcbadcbadcbadcbadcbadcba'

Output: 104860361

Explanation:
There are 3104860382 different non-empty palindromic subsequences, which is 104860361 modulo 10^9 + 7.
```

**Note:**

The length of `S`will be in the range`[1, 1000]`.

Each character`S[i]`will be in the set`{'a', 'b', 'c', 'd'}`.

这个题跟上个题不一样的地方在于，这个题是subsequence字符之间不需要是连着，而上个题是substring字符之间必须要连着。  
且这个题解跟解之间character不能相同，而上个题是位置不能相同。所以不是一道题也不能用一个思路。

这个题可以套用区间DP来解，方程及其复杂，分析来自花花酱：

[http://zxi.mytechroad.com/blog/dynamic-programming/leetcode-730-count-different-palindromic-subsequences](http://zxi.mytechroad.com/blog/dynamic-programming/leetcode-730-count-different-palindromic-subsequences/![]%28http://zxi.mytechroad.com/blog/wp-content/uploads/2017/11/730-ep114-2.png%29以下代码leetcode并过不了。。。但是足够了我觉得)![](http://zxi.mytechroad.com/blog/wp-content/uploads/2017/11/730-ep114-2.png)

以下代码并过不了 但是我觉得足够了

```
class Solution(object):
    def countPalindromicSubsequences(self, S):
        """
        :type S: str
        :rtype: int
        """
        n = len(S)
        self.S = S
        self.dp = [[0 for _ in xrange(n)] for _ in xrange(n)]
        self.flag = [[False for _ in xrange(n)] for _ in xrange(n)]
        return self.msearch(0, n - 1)
    def msearch(self, i, j):
        if self.flag[i][j]:
            return self.dp[i][j]
        self.flag[i][j] = True
        if i > j:
            return self.dp[i][j]
        if i == j:
            self.dp[i][j] = 1
        elif i + 1 == j:
            self.dp[i][j] = 2
        elif self.S[i] != self.S[j]:
            self.dp[i][j] = (self.msearch(i + 1, j) + self.msearch(i, j - 1) \
                    - self.msearch(i + 1, j - 1)) % 1000000007
        else:
            num = (self.msearch(i + 1, j - 1) * 2) % 1000000007
            cnt = self.count(self.S[i], self.S[i + 1: j])
            if cnt == 0:
                num = (num + 2) % 1000000007
            elif cnt == 1:
                num = (num + 1) % 1000000007
            else:
                l, r = self.S[i + 1: j].find(self.S[i]) + i + 1, self.S[i + 1: j].rfind(self.S[i]) + i + 1
                print l, r
                num = num - self.msearch(l + 1, r - 1)
            self.dp[i][j] = num
        return self.dp[i][j]
    def count(self, target, s):
        ans = 0
        for c in s:
            if target == c:
                ans += 1
        return ans
```



