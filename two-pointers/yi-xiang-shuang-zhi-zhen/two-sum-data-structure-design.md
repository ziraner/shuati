Two Sum - Data structure design 解题报告

Design and implement a TwoSum class. It should support the following operations:`add`and`find`.

`add`- Add the number to an internal data structure.  
`find`- Find if there exists any pair of numbers which sum is equal to the value.

  
**Example**

```
add(1); add(3); add(5);
find(4) // return true
find(7) // return false
```

Idea: 

Two Sum变种，用Hash做。

注意统计数字出现的次数，Corner Case为数据结构中只有一个3，target = 6

```
class TwoSum(object):
    
    def __init__(self):
        # initialize your data structure here
        self.map = {}

    # Add the number to an internal data structure.
    # @param number {int}
    # @return nothing
    def add(self, number):
        # Write your code here
        if number not in self.map:
            self.map[number] = 1
        else:
            self.map[number] += 1


    # Find if there exists any pair of numbers which sum is equal to the value.
    # @param value {int}
    # @return true if can be found or false
    def find(self, value):
        # Write your code here
        for num in self.map.keys():
            diff = value - num
            if diff == num:
                if self.map[num] > 1:
                    return True
                continue
            if diff in self.map:
                return True
        return False
```



