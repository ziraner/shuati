Rehashing 解题报告

The size of the hash table is not determinate at the very beginning. If the total size of keys is too large \(e.g. size &gt;= capacity / 10\), we should double the size of the hash table and rehash every keys. Say you have a hash table looks like below:

`size=3`,`capacity=4`

```
[null, 21, 14, null]
       ↓    ↓
       9   null
       ↓
      null
```

The hash function is:

```
int hashcode(int key, int capacity) {
    return key % capacity;
}
```

here we have three numbers, 9, 14 and 21, where 21 and 9 share the same position as they all have the same hashcode 1 \(21 % 4 = 9 % 4 = 1\). We store them in the hash table by linked list.

rehashing this hash table, double the capacity, you will get:

`size=3`,`capacity=8`

```
index:   0    1    2    3     4    5    6   7
hash : [null, 9, null, null, null, 21, 14, null]
```

Given the original hash table, return the new hash table after rehashing .

##### Notice

For negative integer in hash table, the position can be calculated as follow:

* **C++/Java** if you directly calculate -4 % 3 you will get -1. You can use function: a % b = \(a % b + b\) % b to make it is a non negative integer.
* **Python** you can directly use -1 % 3, you will get 2 automatically.

思路：这个题既是考察open hashing又是考察rehashing。注意如果一个node上有1-&gt;...-&gt;3 rehashing后假设1和3还在一起，那么顺序也应该是1-&gt;3而不是3-&gt;1

对于每个旧的idx上的node，计算出新的idx，然后用dummy.next指向新idx的头部，然后将node.val插入新idx的链表尾部，然后新ht的新idx上面的node是dummy.next，然后node = node.next

```
"""
Definition of ListNode
class ListNode(object):

    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""
class Solution:
    """
    @param hashTable: A list of The first node of linked list
    @return: A list of The first node of linked list which have twice size
    """
    def rehashing(self, hashTable):
        # write your code here
        size = 2 * len(hashTable)
        ht = [None for _ in xrange(size)]
        for old_node in hashTable:
            while old_node:
                new_idx = old_node.val % size
                dummy = ListNode(-1)
                dummy.next = ht[new_idx]
                curt = dummy
                while curt.next:
                    curt = curt.next
                curt.next = ListNode(old_node.val)
                ht[new_idx] = dummy.next
                old_node = old_node.next
        return ht
```

  


