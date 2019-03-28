Merge k Sorted Lists 解题报告

Mergeksorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Idea:

解法一：

divide and conquer

把原问题转化成两个子问题，然后合并

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        n = len(lists)
        if n == 0:
            return None
        if n == 1:
            return lists[0]
        left = self.mergeKLists(lists[:n / 2])
        right = self.mergeKLists(lists[n / 2:])
        if left and right:
            return self.merge(left, right)
        if left:
            return left
        if right:
            return right
        return None

    def merge(self, l1, l2):
        dummy = ListNode(0)
        curt = dummy
        while l1 and l2:
            if l1.val < l2.val:
                curt.next = l1
                l1 = l1.next
            else:
                curt.next = l2
                l2 = l2.next
            curt = curt.next
        if l1:
            curt.next = l1
        if l2:
            curt.next = l2
        return dummy.next
```

解法二：

heap

```
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        from heapq import heappush, heappop
        h = []
        for node in lists:
            if node:
                heappush(h, [node.val, node])
        dummy = ListNode(0)
        curt = dummy
        while h:
            val, node = heappop(h)
            curt.next = node
            curt = curt.next
            if node.next:
                heappush(h, [node.next.val, node.next])
        return dummy.next
```



