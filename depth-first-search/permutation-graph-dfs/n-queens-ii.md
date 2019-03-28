N-Queens II解题报告

Follow up for N-Queens problem.

Now, instead outputting board configurations, return the total number of distinct solutions.

  
**Example**

For n=4, there are 2 distinct solutions.

思路依旧dfs，这次递归的是sum

```
class Solution:
    """
    @param: n: The number of queens.
    @return: The total number of distinct solutions.
    """
    def totalNQueens(self, n):
        # write your code here
        self.sum = 0
        sol = []
        self.dfs(sol, n)
        return self.sum
    def dfs(self, sol, n):
        if len(sol) == n:
            self.sum += 1
            return
        for j in xrange(n):
            if self.isValid(sol, j):
                sol.append(j)
                self.dfs(sol, n)
                sol.pop()
    def isValid(self, sol, j):
        j_row = len(sol)
        for i_row, i in enumerate(sol):
            if i == j:
                return False
            if i - i_row == j - j_row:
                return False
            if i + i_row == j + j_row:
                return False
        return True

```



