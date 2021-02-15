Knight Shortest Path 解题报告

Given a knight in a chessboard \(a binary matrix with`0`as empty and`1`as barrier\) with a`source`position, find the shortest path to a`destination`position, return the length of the route.  
Return`-1`if knight can not reached.

**Notice**

source and destination must be empty.  
Knight can not enter the barrier.

**Clarification**

If the knight is at \(_x_,_y_\), he can get to the following positions in one step:

```
(x + 1, y + 2)
(x + 1, y - 2)
(x - 1, y + 2)
(x - 1, y - 2)
(x + 2, y + 1)
(x + 2, y - 1)
(x - 2, y + 1)
(x - 2, y - 1)
```

**Example**

```
[[0,0,0],
 [0,0,0],
 [0,0,0]]
source = [2, 0] destination = [2, 2] return 2

[[0,1,0],
 [0,0,0],
 [0,0,0]]
source = [2, 0] destination = [2, 2] return 6

[[0,1,0],
 [0,0,1],
 [0,0,0]]
source = [2, 0] destination = [2, 2] return -1
```

level order BFS

```
# Definition for a point.
# class Point:
#     def __init__(self, a=0, b=0):
#         self.x = a
#         self.y = b

class Solution:
    # @param {boolean[][]} grid a chessboard included 0 (False) and 1 (True)
    # @param {Point} source a point
    # @param {Point} destination a point
    # @return {int} the shortest path
    def shortestPath(self, grid, source, destination):
        # Write your code here
        # corner case:
        if not grid or not grid[0] or not source or \
                not destination:
            return -1
        if not self.inBound(grid, source.x, source.y) or not \
                self.inBound(grid, destination.x, destination.y):
            return -1
        if grid[destination.x][destination.y] == 1:
            return -1

        deltax = [1, 1, -1, -1, 2, 2, -2, -2]
        deltay = [2, -2, 2, -2, 1, -1, 1, -1]

        queue = [source]
        moves = 0
        while queue:
            size = len(queue)
            for i in range(size):
                tmp = queue.pop(0)
                x, y = tmp.x, tmp.y
                if destination.x == x and destination.y == y:
                    return moves
                for j in range(len(deltax)):
                    newx = x + deltax[j]
                    newy = y + deltay[j]
                    if not self.inBound(grid, newx, newy):
                        continue
                    if grid[newx][newy]:
                        continue
                    queue.append(Point(newx, newy))
                    grid[newx][newy] = 1
            moves += 1
        return -1

    def inBound(self, grid, x, y):
        m = len(grid)
        n = len(grid[0])
        if x < 0 or x >= m or y < 0 or y >= n:
            return False
        return True
```
