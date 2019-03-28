Implement strStr\(\) 解题报告

Implement[strStr\(\)](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or**-1**if needle is not part of haystack.

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

Idea:

Brute Force: O\(m\*n\) 不能AC超时了

```
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        #return haystack.find(needle)
        if not needle:
            return 0
        if not haystack:
            return -1
        # brute force cannot pass
        m, n = len(haystack), len(needle)
        for i in xrange(m):
            if haystack[i] != needle[0]:
                continue
            for j in xrange(min(n, m - i)):
                if j == n - 1 and haystack[i + j] == needle[j]:
                    return i
                if haystack[i + j] != needle[j]:
                    break
        return -1
```

Hash: O\(m + n\) 可以AC虽然基本没beat任何AC的答案

这个题目用到了hash function的实现，我们自己将字符串hash然后通过寻找相同的值来判断小字符串是否存在大字符串中  
同时这个题目也用到了fixed window sum，这里需要注意的是因为hash过所以不能直接减需要减掉val \* baseofhash

Rolling Hash: build a hash base and hashing with it within a fixed window

For python needs to make sure the target, base, and value to be positive any time by adding it to mod

1.calculate the hashing value of the needle as target

2.calculate the base for the window of the needle

3.rolling within the haystack with a fixed window, calculate hashing, if it matches the target then return

Try to pick a mod and a base to be as large and irregular as possible so that we could assume no two different strings end in the same value

```
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        #return haystack.find(needle)
        if not needle:
            return 0
        if not haystack:
            return -1
        # rolling hash O(n + m)
        from sys import maxint
        mod = maxint / 33
        m, n = len(haystack), len(needle)
        target = 0
        for c in needle:
            target = (target * 33 + ord(c) - ord('a')) % mod
            if target < 0:
                target += mod
        base33 = 1
        for i in xrange(n - 1):
            base33 = base33 * 33 % mod
            if base33 < 0:
                base33 += mod
        value = 0
        for i in xrange(m):
            if i >= n:
                value = (value - base33 * (ord(haystack[i - n]) - ord('a'))) % mod
            value = (value * 33 + ord(haystack[i]) - ord('a')) % mod
            if value < 0:
                value += mod
            if i + 1 >= n and value == target:
                return i - n + 1
        return -1
```

KMP: 没看没必要 只有傻吊才专门考KMP

