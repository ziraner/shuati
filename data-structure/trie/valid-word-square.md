Valid Word Square解题报告

Given a sequence of words, check whether it forms a valid word square.

A sequence of words forms a valid word square if thekthrow and column read the exact same string, where 0 ≤k&lt; max\(numRows, numColumns\).

**Note:**

1. The number of words given is at least 1 and does not exceed 500.
2. Word length will be at least 1 and does not exceed 500.
3. Each word contains only lowercase English alphabet`a-z`.

**Example 1:**

```
Input:

[ "abcd",
  "bnrt",
  "crmy",
  "dtye"]

Output:true

Explanation:
The first row and first column both read "abcd".
The second row and second column both read "bnrt".
The third row and third column both read "crmy".
The fourth row and fourth column both read "dtye".
Therefore, it is a valid word square.
```

**Example 2:**

```
Input:

[ "abcd",
  "bnrt",
  "crm",
  "dt"]

Output: true

Explanation:
The first row and first column both read "abcd".
The second row and second column both read "bnrt".
The third row and third column both read "crm".
The fourth row and fourth column both read "dt".
Therefore, it is a valid word square.
```

思路：这个题是word squares的一个小弟题目，corner case很多注意判断

1. 每一个word的长度如果大于words的长度
2. 对j &gt;= len\(words\[i\]\)时，i如果小于len\(word\[j\]\)
3. 对j &lt; len\(word\[i\]\)时，i如果大于等于len\(word\[j\]\)或者两者不相等

```
class Solution(object):
    def validWordSquare(self, words):
        """
        :type words: List[str]
        :rtype: bool
        """
        if not words or not words[0]:
            return True
        n = len(words)
        for i in xrange(n):
            if len(words[i]) > n:
                return False
            for j in xrange(i):
                if j < len(words[i]):
                    if i >= len(words[j]):
                        return False
                    if words[i][j] != words[j][i]:
                        return False
                else:
                    if i < len(words[j]):
                        return False
        return True
```

  


  


  


