Heap

原理：是一个二叉树，root永远比两个儿子大/小，但是两个儿子之间无法比较，必须先填满左儿子才能填右儿子。

heap的考点基本都是如何应用，几乎不会考实现，如果考的话也仅限heapify，即siftup和siftdown两个操作。

Heap上的操作：  
看头部top\(\): O\(1\)  
插入push\(\)：O\(logn\)  
弹出头pop\(\)：O\(logn\)  
删除任意节点remove\(\)：一般heap是O\(n\)，如果key值是唯一的话，hashheap可以做到O\(logn\)的remove

