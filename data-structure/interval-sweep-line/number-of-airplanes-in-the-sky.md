Number of Airplanes in the Sky 解题报告

Given an interval list which are flying and landing time of the flight. How many airplanes are on the sky at most?

##### Notice

If landing and flying happens at the same time, we consider landing should happen at first.

**Example**

For interval list

```
[
  [1,10],
  [2,3],
  [5,8],
  [4,7]
]
```

Return`3`

idea:

扫描线：飞机数目有变化的点其实是interval的端点。将端点保存到数据结构中，然后按照time扫描一遍cnt，遇到降落-1，遇到起飞+1，记录最大的cnt即为answer

对于数据结构有两种构造方法，一种是保存在map里，一种是保存在array里

Map:

```
class Solution:
    """
    @param: airplanes: An interval array
    @return: Count of airplanes are in the sky.
    """
    def countOfAirplanes(self, airplanes):
        # write your code here
        if not airplanes:
            return 0
        # using hashmap
        hm = {}
        for airplane in airplanes:
            if airplane.start in hm: 
                hm[airplane.start] += 1
            else: 
                hm[airplane.start] = 1
            if airplane.end in hm: 
                hm[airplane.end] -= 1
            else: 
                hm[airplane.end] = -1
        ans, cnt = 0, 0
        for i in sorted(hm.keys()):
            cnt += hm[i]
            ans = max(ans, cnt)
        return ans
```

Array:

```
class Solution:
    """
    @param: airplanes: An interval array
    @return: Count of airplanes are in the sky.
    """
    def countOfAirplanes(self, airplanes):
        # write your code here
        if not airplanes:
            return 0
        # using array
        t = []
        for airplane in airplanes:
            t.append([airplane.start, 1])
            t.append([airplane.end, -1])
        t.sort(key = lambda x: (x[0], x[1]))
        ans, cnt = 0, 0
        for _, status in t:
            cnt += status
            ans = max(ans, cnt)
        return ans
```



