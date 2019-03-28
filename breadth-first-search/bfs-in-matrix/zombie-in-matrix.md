Zombie in Matrix解题报告

Given a 2D grid, each cell is either a wall`2`, a zombie`1`or people`0`\(the number zero, one, two\).Zombies can turn the nearest people\(up/down/left/right\) into zombies every day, but can not through wall. How long will it take to turn all people into zombies? Return`-1`if can not turn all people into zombies.

**Example**

Given a matrix:

```
0 1 2 0 0
1 0 0 2 1
0 1 0 0 0

```

return`2`

先统计people的人数并且将zombie入列，然后对zombie做level order bfs。如果people为0则返回天数，否则队列为空返回-1  


```
class Solution:
    # @param {int[][]} grid  a 2D integer grid
    # @return {int} an integer
    def zombie(self, grid):
        # Write your code here
        PEOPLE = 0
        ZOMBIE = 1
        WALL = 2

        deltax = [0, 0, -1, 1]
        deltay = [1, -1, 0, 0]

        m = len(grid)
        n = len(grid[0])

        people = 0
        queue = []
        for i in range(m):
            for j in range(n):
                if grid[i][j] == PEOPLE:
                    people += 1
                elif grid[i][j] == ZOMBIE:
                    queue.append([i, j])

        days = 0
        while queue:
            size = len(queue)
            days += 1
            for i in range(size):
                x, y = queue.pop(0)
                for j in range(len(deltax)):
                    newx = deltax[j] + x
                    newy = deltay[j] + y
                    if newx < 0 or newx >= m or newy < 0 or newy >=n:
                        continue
                    if grid[newx][newy] == PEOPLE:
                        grid[newx][newy] = ZOMBIE
                        queue.append([newx, newy])
                        people -= 1
            if people == 0:
                return days
        return -1
```



