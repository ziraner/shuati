Remove Invalid Parentheses 解题报告

Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

Note: The input string may contain letters other than the parentheses`(`and`)`.

**Examples:**

```
"()())()" -> ["()()()", "(())()"]
"(a)())()" -> ["(a)()()", "(a())()"]
")(" -> [""]
```

Idea:

DFS 

DFS中for循环遍历当前string删掉哪个括号，剪枝的时候剪掉当前位置不是括号的，新生成的string visited过的，新生成的string mismatch跟原来一样或者还TM多的

这个做法不需要考虑valid但是删除多了的情况，因为那种情况一定是在某个stage 生成的mismatch跟原来相等或者还TM多的，已经在剪枝过程中被剪掉了

需要每次修改visited，但是不需要修改回去。

```
class Solution:
    def removeInvalidParentheses(self, s):
        visited = set([s])
        ans = []
        self.helper(s, ans, visited)
        return ans
    def helper(self, s, ans, visited):
        if self.calcMismatches(s) == 0:
            ans.append(s)
            return
        for i in xrange(len(s)):
            if s[i] not in '()':
                continue
            new_s = s[:i] + s[i + 1:]
            if new_s in visited:
                continue
            if self.calcMismatches(new_s) >= self.calcMismatches(s):
                continue
            visited.add(new_s)
            self.helper(new_s, ans, visited)
    def calcMismatches(self, s):
        left, right = 0, 0
        for i in xrange(len(s)):
            if s[i] == '(':
                left += 1
            elif s[i] == ')':
                if left == 0:
                    right += 1
                else:
                    left -= 1
        return left + right
```

以上程序比较主要的是calcMismatches函数，是valid括号问题的一个比较general的基本功。里面left是多余的左括号数量，right是多余的右括号数量。

Facebook可能会先问下这个题目的简单版本，给出任意一个solution就OK。

我们可以利用以上calcMismatches函数制定自己的solution。

计算出left和right之后，从右向左移除left个左括号，从左向右移除right个右括号，这样可以保证剩下的一定是valid。代码如下

```
class Solution:
    def removeInvalidParentheses(self, s):
        left, right = 0, 0
        for i in xrange(len(s)):
            if s[i] == '(':
                left += 1
            elif s[i] == ')':
                if left == 0:
                    right += 1
                else:
                    left -= 1
        s1 = ''
        for i in xrange(len(s)):
            if s[i] == ')' and right != 0:
                right -= 1
                continue
            s1 += s[i]
        s2 = ''
        for i in xrange(len(s1) - 1, -1, -1):
            if s1[i] == '(' and left != 0:
                left -= 1
                continue
            s2 = s1[i] + s2
        return s2
```



