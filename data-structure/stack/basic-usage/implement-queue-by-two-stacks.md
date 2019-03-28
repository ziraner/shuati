Implement Queue by Two Stacks 解题报告  
As the title described, you should only use two stacks to implement a queue's actions.

The queue should support`push(element)`,`pop()`and`top()`where pop is pop the first\(a.k.a front\) element in the queue.

Both pop and top methods should return the value of first element.

  
**Example**

```
push(1)
pop()     // return 1
push(2)
push(3)
top()     // return 2
pop()     // return 2

```

```
class MyQueue(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.stack1, self.stack2 = [], []

    def push(self, x):
        """
        Push element x to the back of queue.
        :type x: int
        :rtype: void
        """
        self.stack1.append(x)
        

    def pop(self):
        """
        Removes the element from in front of queue and returns that element.
        :rtype: int
        """
        if self.empty():
            return -1
        if not self.stack2:
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        return self.stack2.pop()

    def peek(self):
        """
        Get the front element.
        :rtype: int
        """
        if self.empty():
            return -1
        if not self.stack2:
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        return self.stack2[-1]

    def empty(self):
        """
        Returns whether the queue is empty.
        :rtype: bool
        """
        return not self.stack1 and not self.stack2


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()

```



