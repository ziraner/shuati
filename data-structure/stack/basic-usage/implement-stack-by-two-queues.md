Implement Stack by Two Queues 解题报告

Implement a stack by two queues. The queue is first in first out \(FIFO\). That means you can not directly pop the last element in a queue.  
**Example**

```
push(1)
pop()
push(2)
isEmpty() // return false
top() // return 2
pop()
isEmpty() // return true

```

用两个q模拟stack

pop的时候每次把第一个q pop到只有一个量，然后pop出来的放入第二个q，最后再把这俩q换下  
push的时候就直接塞进第一个q

```
class Stack:
    # initialize your data structure here.
    def __init__(self):
        self.q1 = []
        self.q2 = []

    # @param x, an integer, push a new item into the stack
    # @return nothing
    def push(self, x):
        # Write your code here
        self.q1.append(x)

    # @return nothing, pop the top of the stack
    def pop(self):
        # Write your code here
        while len(self.q1) != 1:
            self.q2.append(self.q1.pop(0))
        self.q1.pop(0)
        self.q1, self.q2 = self.q2, self.q1

    # @return an integer, return the top of the stack
    def top(self):
        # Write your code here
        while len(self.q1) != 1:
            self.q2.append(self.q1.pop(0))
        item = self.q1.pop(0)
        self.q1, self.q2 = self.q2, self.q1
        self.q1.append(item)
        return item
    # @return an boolean, check the stack is empty or not.
    def isEmpty(self):
        # Write your code here
        return len(self.q1) == 0
```

  


