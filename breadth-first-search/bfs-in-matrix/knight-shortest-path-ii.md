Knight Shortest Path II 解题报告

Given a knight in a chessboard`n * m`\(a binary matrix with 0 as empty and 1 as barrier\). the knight initialze position is`(0, 0)`and he wants to reach position`(n - 1, m - 1)`, Knight can only be from left to right. Find the shortest path to the destination position, return the length of the route. Return`-1`if knight can not reached.

**Clarification**

If the knight is at \(x, y\), he can get to the following positions in one step:

```
(x + 1, y + 2)
(x - 1, y + 2)
(x + 2, y + 1)
(x - 2, y + 1)
```

**Example**

```
[[0,0,0,0],
 [0,0,0,0],
 [0,0,0,0]]

Return 3

[[0,0,0,0],
 [0,0,0,0],
 [0,1,0,0]]

Return -1
```

这个题目可以用BFS来做，是Knight Shortest Path I的一个特殊情况，也可以用DP来做，时间复杂度级数上相同的，都是最坏情况遍历一遍所有的矩阵中的点，但是DP慢因为要遍历四遍矩阵最差情况

这个题用接龙型DP比较简单的点在于前面只能从四个地方走到这里，所以对每个i,j只需要循环四下就OK了

```
from sys import maxint


class Solution:
    """
    @param: grid: a chessboard included 0 and 1
    @return: the shortest path
    """
    def shortestPath2(self, grid):
        # write your code here
        # solution1: bfs special case of kspI, src = 0,0, dst= n-1, m-1
        # solution2: æ¥é¾åDP: f[i][j]åé¢ä»»æä¸ç¹å°i,jç»æçæå°æ­¥éª¤
        if not grid or not grid[0]:
            return -1
        n = len(grid)
        m = len(grid[0])
        f = [[maxint for _ in range(m)] for _ in range(n)]
        if grid[0][0] == 1 or grid[n - 1][m - 1] == 1:
            return -1
        f[0][0] = 0
        # always go to the right
        delta = [[1, 2], [-1, 2], [2, 1], [-2, 1]]
        # loop y first because y is always increasing
        for j in range(m):
            for i in range(n):
                if grid[i][j]:
                    continue
                for deltax, deltay in delta:
                    prev_i = i - deltax
                    prev_j = j - deltay
                    if not self.inBound(prev_i, prev_j, n, m):
                        continue
                    if f[prev_i][prev_j] == maxint:
                        continue
                    f[i][j] = min(f[i][j], f[prev_i][prev_j] + 1)
        if f[n - 1][m - 1] == maxint:
            return -1
        return f[n -1][m - 1]

    def inBound(self, x, y, n, m):
        if x < 0 or y < 0 or x >=n or y >= m:
            return False
        return True
```



