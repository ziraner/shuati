Brick Wall 解题报告

There is a brick wall in front of you. The wall is rectangular and has several rows of bricks. The bricks have the same height but different width. You want to draw a vertical line from the **top **to the **bottom **and cross the **least **bricks.

The brick wall is represented by a list of rows. Each row is a list of integers representing the width of each brick in this row from left to right.

If your line go through the edge of a brick, then the brick is not considered as crossed. You need to find out how to draw the line to cross the least bricks and return the number of crossed bricks.

**You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.**  
**Example:**

```
Input:

[[1,2,2,1],
 [3,1,2],
 [1,3,2],
 [2,4],
 [3,1,2],
 [1,3,1,1]]

Output: 2

Explanation
```

![](https://leetcode.com/static/images/problemset/brick_wall.png)  
Idea:

这个题其实想想可能算是sweepline问题，但是只需要统计end就可以了

建立一个hashmap统计end出现的个数，end出现的最多的就是我们需要cut的地方

需要注意的地方在于

1.不能把最后面的end加进去

2.Corner case: \[\[1\], \[1\], \[1\]\]我们需要返回wall的长度

```
class Solution(object):
    def leastBricks(self, wall):
        """
        :type wall: List[List[int]]
        :rtype: int
        """
        end_cnt = {}
        for bricks in wall:
            end = 0
            final_end = sum(bricks)
            for brick in bricks:
                end += brick
                if end == final_end:
                    break
                if end not in end_cnt:
                    end_cnt[end] = 1
                else:
                    end_cnt[end] += 1
        if end_cnt:
            return len(wall) - max(end_cnt.values())
        return len(wall)
```



