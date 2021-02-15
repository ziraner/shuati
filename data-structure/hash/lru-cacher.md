LRU Cache 解题报告

Design and implement a data structure for Least Recently Used \(LRU\) cache. It should support the following operations: `get` and `set`.

`get(key)` - Get the value \(will always be positive\) of the key if the key exists in the cache, otherwise return -1.  
`set(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

方法一：doublylinkedlist & hashmap  
dict = {key: current node}; DoublyLinkedList: val, key, prev, next.  
Cache: head, tail = node, node; head.next = tail, tail.prev = head

```python
class LRUCache(object):

    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.head, self.tail = DoublyLinkedList(-1, -1), DoublyLinkedList(-1, -1)
        self.cap = capacity
        self.head.next, self.tail.prev = self.tail, self.head
        self.hm = {}
    def get(self, key):
        """
        :type key: int
        :rtype: int
        """
        if key not in self.hm:
            return -1
        node = self.hm[key]
        node.prev.next = node.next
        node.next.prev = node.prev
        self.move_to_tail(node)
        return node.val

    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: void
        """
        if self.get(key) != -1:
            self.hm[key].val = value
            return
        if self.cap == len(self.hm):
            del self.hm[self.head.next.key]
            self.head.next = self.head.next.next
            self.head.next.prev = self.head

        node = DoublyLinkedList(key, value)
        self.hm[key] = node
        self.move_to_tail(node)

    def move_to_tail(self, node):
        tmp = self.tail.prev
        self.tail.prev = node
        node.next = self.tail
        node.prev = tmp
        tmp.next = node

class DoublyLinkedList:
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.next = self.prev = None



# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

方法二：

SinglyLinkedList + HashMap

dict = {key: previous node}; SinglyLinkedList: val, key, next.  
Cache: head = tail = node

经验是 不要写好几个函数，就把代码写在要求的函数里，好整。每次删完了node需要判断是否是tail

```python
class LRUCache(object):

    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.head = self.tail = SinglyListNode(-1, -1)
        self.hm = {}
        self.cap = capacity


    def get(self, key):
        """
        :type key: int
        :rtype: int
        """
        if key not in self.hm:
            return -1
        prev = self.hm[key]
        node = prev.next
        prev.next = node.next
        if prev.next:
            self.hm[prev.next.key] = prev
        else:
            self.tail = prev

        self.hm[node.key] = self.tail
        self.tail.next = node
        node.next = None
        self.tail = node

        return node.val

    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: void
        """
        if self.get(key) != -1:
            self.hm[key].next.val = value
            return

        if len(self.hm) == self.cap:
            del self.hm[self.head.next.key]
            self.head.next = self.head.next.next
            if self.head.next:
                self.hm[self.head.next.key] = self.head
            else:
                self.tail = self.head

        node = SinglyListNode(key, value)
        self.hm[key] = self.tail
        self.tail.next = node
        self.tail = node


class SinglyListNode:
    def __init__(self, key, val):
        self.next = None
        self.key = key
        self.val = val

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
