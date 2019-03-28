Palindromic Substrings 解题报告

Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1:**

```
Input: "abc"

Output: 3

Explanation: Three palindromic strings: "a", "b", "c".
```

**Example 2:**

```
Input: "aaa"

Output: 6

Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```

Idea:

用BFS时间复杂度跟subsets是一样的O\(2^n\)

```
class Solution(object):
    def countSubstrings(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s:
            return 0
        n = len(s)
        q = []
        for i in xrange(n):
            q.append((i, i))
        for i in xrange(1, n):
            if s[i] == s[i - 1]:
                q.append((i - 1, i))
        ans = 0
        while q:
            i, j = q.pop(0)
            ans += 1
            left, right = i - 1, j + 1
            if left >= 0 and right < n and s[left] == s[right]:
                q.append((left, right))
        return ans
```



