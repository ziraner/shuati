Palindrome Partitioning II解题报告

Given a string_s_, cut_s_into some substrings such that every substring is a palindrome.

Return the**minimum**cuts needed for a palindrome partitioning of_s_.

**Example**

Given s =`"aab"`,

Return`1`since the palindrome partitioning \["aa", "b"\] could be produced using_1_cut.

一个简单的想法是DFS，跟palindrome partitioning一样但是时间复杂度过于高过不了

```
class Solution:
    # @param s, a string
    # @return an integer
    def minCut(self, s):
        # write your code here
        # dfs guo bu liao
        """
        from sys import maxint
        self.min = maxint
        isP = self.getPalindrome(s)
        sol = []
        self.dfs(sol, s, 0, isP)
        return self.min
    def dfs(self, sol, s, pos, isP):
        if pos == len(s):
            self.min = min(self.min, len(sol) - 1)
            return
        for i in xrange(pos, len(s)):
            if isP[pos][i]:
                sol.append(s[pos: i + 1])
                self.dfs(sol, s, i + 1, isP)
                sol.pop()
    def getPalindrome(self, s):
        n = len(s)
        isP = [[False for _ in xrange(n)] for _ in xrange(n)]
        for i in xrange(n):
            for j in xrange(i, n):
                if self.isPalindrome(s[i:j + 1]):
                    isP[i][j] = True
        return isP
    def isPalindrome(self, s):
        n = len(s)
        for i in xrange(n / 2):
            if s[i] != s[n - i - 1]:
                return False
        return True
```

然后DP可以过

```
class Solution:
    # @param s, a string
    # @return an integer
    def minCut(self, s):
        # write your code here
        # dp
        from sys import maxint
        n = len(s)
        #isP = self.getPalindrome(s)
        f = [maxint for _ in xrange(n + 1)]
        f[0] = 0
        for i in xrange(1, n + 1):
            for j in xrange(i):
                if self.isPalindrome(s[j:i]):
                    f[i] = min(f[i], f[j] + 1)
        return f[n] - 1
    def isPalindrome(self, s):
        n = len(s)
        for i in xrange(n / 2):
            if s[i] != s[n - i - 1]:
                return False
        return True
```



