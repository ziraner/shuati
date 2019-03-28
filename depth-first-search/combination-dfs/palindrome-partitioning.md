Palindrome Partitioning 解题报告

Given a string_s_, partition_s_such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.  
**Example**

Given s =`"aab"`, return:

```
[
  ["aa","b"],
  ["a","a","b"]
]

```

  
DFS问题，

需要一个预处理数组，判断当前i到j，i，j都是包含关系，是不是palindrome

```
class Solution:
    # @param s, a string
    # @return a list of lists of string
    def partition(self, s):
        # write your code here
        if not s:
            return []

        str_list = []
        result = []
        isP = self.getPalindrome(s)
        self.dfs(s, isP, 0, str_list, result)
        return result

    def dfs(self, s, isP, startIndex, str_list, result):
        if startIndex == len(s):
            result.append(str_list[:])
            return
        for i in range(startIndex, len(s)):
            if not isP[startIndex][i]:
                continue
            str_list.append(s[startIndex:i + 1])
            self.dfs(s, isP, i + 1, str_list, result)
            str_list.pop()
            
        
    def getPalindrome(self, s):
        length = len(s)
        isP = [[0 for _ in range(length)] for _ in range(length)]
        for i in range(length):
            for j in range(i, length):
                if self.isPalindrome(s[i:j + 1]):
                    isP[i][j] = 1
        return isP

    def isPalindrome(self, str):
        length = len(str)
        for i in range(length / 2):
            if str[i] != str[length - 1 - i]:
                return False
        return True
```



