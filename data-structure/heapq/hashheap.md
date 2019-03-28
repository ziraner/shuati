HashHeap 解题报告

没有这么一个题目，但是Sliding Window Median和Building Outline都用到了hashheap的实现

push\(\): O\(logn\) 把元素放到array最后，然后siftup

pop\(\): O\(logn\) 把root和最后一个元素对调，然后删除最后一个元素，然后siftdown root

top\(\): O\(1\) 看一下root

remove: 通过hash找到节点然后把节点和最后一个节点对调，然后删除最后一个元素，然后siftup，然后siftdown

数据结构

数组self.heap存放的是val

哈希self.hash key: val, value: node

node: id是数组的idx, num是val出现的次数

```
# id is the heap index
# num is the count of numbers the item exists in the heap
class Node:
    def __init__(self, id, num):
        self.id = id
        self.num = num

# min heap
class HashHeap:
    def __init__(self, ):
        self.heap = []
        self.hash = {}
        self.size = 0

    # push only siftup
    def push(self, item):
        self.size += 1
        if item in self.hash:
            self.hash[item].num += 1
        else:
            self.heap.append(item)
            self.hash[item] = Node(len(self.heap) - 1, 1)
        self.siftup(len(self.heap) - 1)

    # pop only siftdown
    def pop(self, ):
        self.size -= 1
        val = self.heap[0]
        if self.hash[val].num == 1:
            self.swap(0, len(self.heap) - 1)
            del self.hash[val]
            self.heap.pop()
            if len(self.heap) > 0:
                self.siftdown(0)
        else:
            self.hash[val].num -= 1
        return val

    # remove siftup and siftdown
    def remove(self, item):
        self.size -= 1
        n = len(self.heap)
        if self.hash[item].num == 1:
            id = self.hash[item].id
            self.swap(id, n - 1)
            del self.hash[item]
            self.heap.pop()
            if len(self.heap) > id:
                self.siftup(id)
                self.siftdown(id)
        else:
            self.hash[item].num -= 1

    def swap(self, id1, id2):
        val1 = self.heap[id1]
        val2 = self.heap[id2]
        num1 = self.hash[val1].num
        num2 = self.hash[val2].num
        #swap heap
        self.heap[id1] = val2
        self.heap[id2] = val1
        # swap hash
        self.hash[val1] = Node(id2, num1)
        self.hash[val2] = Node(id1, num2)

    def siftup(self, id):
        while id >= 1:
            parent_id = (id - 1) / 2
            if self.heap[parent_id] <= self.heap[id]:
                break
            self.swap(parent_id, id)
            id = parent_id

    def siftdown(self, id):
        n = len(self.heap)
        while id < n / 2:
            l_son = id * 2 + 1
            r_son = id * 2 + 2
            smallest = id
            if l_son < n and self.heap[l_son] < self.heap[smallest]:
                smallest = l_son
            if r_son < n and self.heap[r_son] < self.heap[smallest]:
                smallest = r_son
            if smallest == id:
                break
            self.swap(smallest, id)
            id = smallest

    def isEmpty(self, ):
        return self.size == 0

    def top(self, ):
        return self.heap[0]

```



