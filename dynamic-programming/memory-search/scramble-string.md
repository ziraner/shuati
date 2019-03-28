Scramble String解题报告

Given a string`s1`, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.

Below is one possible representation of`s1 = "great"`:

```
    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t

```

To scramble the string, we may choose any non-leaf node and swap its two children.

For example, if we choose the node`"gr"`and swap its two children, it produces a scrambled string`"rgeat"`.

```
    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t

```

We say that`"rgeat"`is a scrambled string of`"great"`.

Similarly, if we continue to swap the children of nodes`"eat"`and`"at"`, it produces a scrambled string`"rgtae"`.

```
    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a

```

We say that`"rgtae"`is a scrambled string of`"great"`.

Given two strings`s1`and`s2`of the same length, determine if`s2`is a scrambled string of`s1`.

区间类+匹配类DP

dp\[x\]\[y\]\[k\] 表示是从s1串x开始，s2串y开始，他们后面k个字符组成的substr是Scramble String

Function:

• 对于所有i属于{1,k}

• s11 = s1.substring\(0, i\); s12 = s1.substring\(i, s1.length\(\)\);

• s21 = s2.substring\(0, i\); s22 = s2.substring\(i, s2.length\(\)\);

• s23 = s2.substring\(0, s2.length\(\) - i\); s24 = s2.substring\(s2.length\(\) - i, s2.length\(\)\);

• for i = x -&gt; x+k

• dp\[x\]\[y\]\[k\] = \(dp\[x\]\[y\]\[i\] && dp\[x+i\]\[y+i\]\[k-i\]\) \|\| dp\[x\]\[y+k-i\]\[i\] && dp\[x+i\]\[y\]\[k-i\]\)

Intialize:

• dp\[i\]\[j\]\[1\] = s1\[i\]==s\[j\].

Answer:

• dp\[0\]\[0\]\[len\]

```
class Solution:
    """
    @param: s1: A string
    @param: s2: Another string
    @return: whether s2 is a scrambled string of s1
    """
    def isScramble(self, s1, s2):
        # write your code here
        # 3D dp: dp[i][j][k] s1:starting from i s2:starting from j, length k
        # for length l in [1, k), s11 s21 & s12 s22 match OR s11 s22 & s12 s21 match
        if not s1 and not s2:
            return True
        n = len(s1)
        if len(s2) != n:
            return False
        self.dp = [[[False for _ in range(n + 1)] for _ in range(n)] for _ in range(n)]
        self.flag = [[[False for _ in range(n + 1)] for _ in range(n)] for _ in range(n)]
        return self.memorysearch(0, 0, n, s1, s2)
    def memorysearch(self, i, j, k, s1, s2):
        if self.flag[i][j][k]:
            return self.dp[i][j][k]
        self.flag[i][j][k] = True
        if k == 1:
            self.dp[i][j][k] = s1[i] == s2[j]
        for l in range(1, k):
            m1 = self.memorysearch(i, j, l, s1, s2)
            m2 = self.memorysearch(i + l, j + l, k - l, s1, s2)
            m3 = self.memorysearch(i, j + k - l, l, s1, s2)
            m4 = self.memorysearch(i + l, j, k - l, s1, s2)
            if m1 and m2 or m3 and m4:
                self.dp[i][j][k] = True
                break
        return self.dp[i][j][k]
```



