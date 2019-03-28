Insert Delete GetRandom O\(1\) 解题报告

Design a data structure that supports all following operations in average **O\(1\)**time.

1. `insert(val)`: Inserts an item val to the set if not already present.
2. `remove(val)`: Removes an item val from the set if present.
3. `getRandom`: Returns a random element from current set of elements. Each element must have the **same probability **of being returned.

Idea:

O\(1\)的insert delete是 hashset or hashmap，但是hashmap不能O\(1\) random。array可以O\(1\) random因为是random index access

所以最后的数据结构就是hashmap + array

```
class RandomizedSet(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.hm = {}
        self.arr = []

    def insert(self, val):
        """
        Inserts a value to the set. Returns true if the set did not already contain the specified element.
        :type val: int
        :rtype: bool
        """
        if val in self.hm:
            return False
        self.hm[val] = len(self.arr)
        self.arr.append(val)
        return True

    def remove(self, val):
        """
        Removes a value from the set. Returns true if the set contained the specified element.
        :type val: int
        :rtype: bool
        """
        if val not in self.hm:
            return False
        idx = self.hm[val]
        self.arr[idx], self.arr[-1] = self.arr[-1], self.arr[idx]
        self.hm[self.arr[idx]] = idx
        self.arr.pop()
        del self.hm[val]
        return True

    def getRandom(self):
        """
        Get a random element from the set.
        :rtype: int
        """
        from random import randint
        idx = randint(0, len(self.arr) - 1)
        return self.arr[idx]
        
# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```

  


