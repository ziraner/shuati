String Permutation II 解题报告

Given a string, find all permutations of it without duplicates.

**Example**

Given`"abb"`, return`["abb", "bab", "bba"]`.

Given`"aabb"`, return`["aabb", "abab", "baba", "bbaa", "abba", "baab"]`.

  
跟经典的permutation差不多，就是从array变成了string

方法一：DFS

```
class Solution:
    """
    @param: str: A string
    @return: all permutations
    """
    def stringPermutation2(self, str):
        # write your code here
        # dfs
        result = []
        c_list = []
        visited = [False for _ in range(len(str))]
        new_str = sorted(str)
        self.dfs(result, c_list, visited, new_str)
        return result
    def dfs(self, result, c_list, visited, str):
        if len(c_list) == len(str):
            result.append(''.join(c_list[:]))
            return
        for i in range(len(str)):
            if visited[i]:
                continue
            if i != 0 and str[i] == str[i - 1] and not visited[i - 1]:
                continue
            c_list.append(str[i])
            visited[i] = True
            self.dfs(result, c_list, visited, str)
            visited[i] = False
            c_list.pop()

```

方法二，用next permutation的题目的程序，一个一个next

```
class Solution:
    """
    @param: str: A string
    @return: all permutations
    """
    def stringPermutation2(self, str):
        # write your code here
        # next permutation
        if not str:
            return [""]
        c_list = list(str)
        c_list.sort()
        result = []
        while True:
            result.append(''.join(c_list[:]))
            c_list = self.nextPermutation(c_list)
            if not c_list:
                break
        return result
    def nextPermutation(self, c_list):
        n = len(c_list)
        i = n - 2
        while i != -1:
            if c_list[i + 1] > c_list[i]:
                break
            i -= 1
        if i == -1: return None
        for j in range(n - 1, i, -1):
            if c_list[j] > c_list[i]:
                c_list[i], c_list[j] = c_list[j], c_list[i]
                break
        return c_list[:i + 1] + c_list[i + 1:][::-1]
```



