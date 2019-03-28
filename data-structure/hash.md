Hash需要会1.原理2.应用

1.原理

Hash Function

Collision:  
Open hashing：插入的时候遇到被占用的保存到下一个不为空的坑；删除了则需要表示为《删除》，否则后面的找不到了；寻找的时候就去找，遇到空的停止，遇到《删除》则去下一个，遇到不为空的则也去下一个直到找到为止。  
Closed hashing：存一链表，array + linkedlist

Rehashing：占有率在10%左右就得rehashing

2.应用

海量用hash的问题  
用hash实现数据结构利用hash的O\(1\)的insert delete find特性 比如LRUCache，Insert Delete Random，

