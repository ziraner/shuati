Longest Palindromic Substring解题报告

Given a string`S`, find the longest palindromic substring in`S`. You may assume that the maximum length of`S`is 1000, and there exists one unique longest palindromic substring.

**Example**

Given the string =`"abcdzdcab"`, return`"cdzdc"`.

思路1：乍一看这个题貌似可以用递归来解，

dp\[i\]\[j\]表示从i到j，包括i，j，是否是不是一个palindrome substring，但是可以发现dp\[i\]\[j\]的解是依赖于i + 1, j - 1的解，更x向是一个区间DP的问题，我们知道区间dp一般为了推倒简单起见都用memorizationsearch所以这个题的记忆化搜索的解法如下：

```
class Solution:
    """
    @param: s: input string
    @return: the longest palindromic substring
    """
    def longestPalindrome(self, s):
        # write your code here
        # dp[i][j] = dp[i + 1][j -1] + 2 if s[i] == s[j]
        if not s:
            return ""
        # O(n2) time and space
        # memorization search
        n = len(s)
        self.dp = [[False for _ in range(n)] for _ in range(n)]
        self.flag = [[False for _ in range(n)] for _ in range(n)]
        self.ans = ""
        self.cur = ""
        for i in range(n):
            for j in range(n - 1, i - 1, -1):
                self.memorysearch(i, j, s)
        return self.ans
    def memorysearch(self, i, j, s):
        if self.flag[i][j]:
            return
        self.flag[i][j] = True
        if i == j:
            self.dp[i][j] = True
            self.cur = s[i]
        elif i + 1 == j:
            if s[i] == s[j]:
                self.dp[i][j] = True
                self.cur = s[i:j + 1]
        else:
            self.memorysearch(i + 1, j - 1, s)
            if s[i] == s[j] and self.dp[i + 1][j - 1]:
                self.cur = s[i] + self.cur + s[j]
                self.dp[i][j] = True
        if len(self.ans) < len(self.cur):
            self.ans = self.cur
```



思路2：这个题可以用DP来做，但是不是最优的，是O\(n^2\)的时间和空间复杂度

dp\[i\]\[j\]表示从i到j，包括i，j，是否是不是一个palindrome substring

这个DP解法的巧妙之处在于一般来说dp都是从小到大的，不能从大到小，而我们算i，j状态的时候需要取决于i + 1, j - 1的状态，乍一看不可行，但是实际上是可行的。

00  
00 01  
     11  
00 01 02  
     11 12  
           22  
00 01 02 03  
     11 12 13  
          22 23  
               33  
其实就是说在算02的时候11已经算完了，再算13的时候22也算完了，所以这个DP递推公式是可行的  
D\[i\]\[j\] = if \(char i == char j\) &&\(D\[i + 1\]\[j - 1\]  \|\|  j - i &lt;= 2\)\)

```
class Solution:
    """
    @param: s: input string
    @return: the longest palindromic substring
    """
    def longestPalindrome(self, s):
        # write your code here
        if not s:
            return ""
        n = len(s)
        dp = [[False for _ in range(n)] for _ in range(n)]
        ans = ""
        for j in range(n):
            for i in range(j + 1):
                dp[i][j] = s[i] == s[j] and (j - i < 2 or dp[i + 1][j - 1])
                if dp[i][j] and j - i + 1 > len(ans):
                    ans = s[i:j + 1]
        return ans
```

这个题也可以用一种很牛逼的处理palindrome的方法来做，就是以i,i或者i-1,i为中心两边扩展，又称中心扩展法

```
class Solution:
    """
    @param: s: input string
    @return: the longest palindromic substring
    """
    def longestPalindrome(self, s):
        # write your code here
        # dp[i][j] = dp[i + 1][j -1] + 2 if s[i] == s[j]
        if not s:
            return ""
        n = len(s)
        ans = ""
        for i in range(n):
            s1 = self.expand(s, i, i)
            s2 = self.expand(s, i, i + 1)
            if len(s1) >= len(ans):
                ans = s1
            if len(s2) >= len(ans):
                ans = s2
        return ans
    def expand(self, s, x, y):
        while x >= 0 and y < len(s):
            if s[x] != s[y]:
                break
            x -= 1
            y += 1
        return s[x + 1: y]
```



