Heapify 解题报告

Given an integer array, heapify it into a min-heap array.

For a heap array A, A\[0\] is the root of heap, and for each A\[i\], A\[i \* 2 + 1\] is the left child of A\[i\] and A\[i \* 2 + 2\] is the right child of A\[i\].

Idea：

这个题目是一道考Heap原理的题目，是栈实现的一个重要的步骤。

heap被用数组来表示，left = k \* 2 + 1, right = k \* 2 + 2, father = \(k - 1\) / 2

一般来说heapify可以siftup和siftdown，单纯一个点siftup和siftdown的时间复杂度都是O\(logn\)。但是在heapify中用siftup是O\(nlogn\)，用siftdown是O\(n\)，至于为什么是O\(n\)，在中点处siftdown有人数学证明过是O\(n\)

siftup代码，需要学习的是怎么写siftup函数

```
class Solution:
    # @param A: Given an integer array
    # @return: void
    def heapify(self, A):
        # write your code here
        # siftup O(nlogn)
        """
        for i in range(len(A)):
            self.siftup(A, i)
    def siftup(self, A, k):
        while k != 0:
            father = (k - 1) / 2
            if A[father] < A[k]:
                break
            A[father], A[k] = A[k], A[father]
            k = father
```

siftdown代码，需要学习的是怎么写siftdown函数

```
class Solution:
    # @param A: Given an integer array
    # @return: void
    def heapify(self, A):
        # write your code here
        for i in range(len(A) / 2, -1, -1):
            self.siftdown(A, i)
    def siftdown(self, A, k):
        while k < len(A):
            smallest = k
            if 2 * k + 1 < len(A) and A[2 * k + 1] < A[smallest]:
                smallest = 2 * k + 1
            if 2 * k + 2 < len(A) and A[2 * k + 2] < A[smallest]:
                smallest = 2 * k + 2
            if smallest == k:
                break
            A[smallest], A[k] = A[k], A[smallest]
            k = smallest

```



