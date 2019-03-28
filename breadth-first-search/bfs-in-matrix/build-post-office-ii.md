Build Post Office II 解题报告

Given a 2D grid, each cell is either a wall`2`, an house`1`or empty`0`\(the number zero, one, two\), find a place to build a post office so that the sum of the distance from the post office to all the houses is smallest.

Return the smallest sum of distance. Return`-1`if it is not possible.

##### Notice

* You cannot pass through wall and house, but can pass through empty.
* You only build post office on an empty.

**Example**

Given a grid:

```
0 1 0 0 0
1 0 0 2 1
0 1 0 0 0

```

return`8`, You can build at`(1,1)`. \(Placing a post office at \(1,1\), the distance that post office to all the house sum is smallest.\)

先统计房子的数目，然后建立两个矩阵，分别记录当前点被访问了多少次visited，以及当前点的dist sum from all post offices  
然后以每个house为起点做level order bfs，经过每个点更新visited和dist sum两个数组。BFS的时候就是矩阵中的level order BFS带visited矩阵。最后再扫一遍矩阵，对每一个空地，先看是否被所有的house都访问过，如果访问过的话，更新ans，否则不更新。

```
class Solution:
    # @param {int[][]} grid a 2D grid
    # @return {int} an integer
    EMPTY, HOUSE, WALL = 0, 1, 2
    m, n = 0, 0
    def shortestDistance(self, grid):
        # Write your code here
        if not grid or not grid[0]:
            return 0

        self.m = len(grid)
        self.n = len(grid[0])

        visited_no = [[0 for _ in range(self.n)] for _ in range(self.m)]
        distance_sum = [[0 for _ in range(self.n)] for _ in range(self.m)]

        house_no = 0
        for i in range(self.m):
            for j in range(self.n):
                if grid[i][j] == self.HOUSE:
                    self.bfs(i, j, grid, visited_no, distance_sum)
                    house_no += 1

        import sys
        shortest = sys.maxint
        for i in range(self.m):
            for j in range(self.n):
                if grid[i][j] == self.EMPTY:
                    if visited_no[i][j] != house_no:
                        continue
                    shortest = min(distance_sum[i][j], shortest)

        if shortest != sys.maxint:
            return shortest
        return -1

    def bfs(self, i, j, grid, visited_no, distance_sum):
        deltax = [-1, 1, 0, 0]
        deltay = [0, 0, -1, 1]
        queue = [[i, j]]
        visited = [[0 for _ in range(self.n)] for _ in range(self.m)]
        visited[i][j] = 1
        level = 0
        while queue:
            size = len(queue)
            level += 1
            for ii in range(size):
                x, y = queue.pop(0)
                for jj in range(len(deltax)):
                    newx = x + deltax[jj]
                    newy = y + deltay[jj]
                    if newx < 0 or newx >= self.m or newy < 0 \
                            or newy >= self.n:
                        continue
                    if visited[newx][newy]:
                        continue
                    if grid[newx][newy] != self.EMPTY:
                        continue
                    queue.append([newx, newy])
                    visited[newx][newy] = 1
                    visited_no[newx][newy] += 1
                    distance_sum[newx][newy] += level


```



