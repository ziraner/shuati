Remove Duplicates from Sorted List

Description:

Given a sorted linked list, delete all duplicates such that each element appear only once.

Example 1:
Input: 1->1->2
Output: 1->2

Example 2:
Input: 1->1->2->3->3
Output: 1->2->3

Idea:
跟array类似，用两个同向指针

Solution:
```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head
        slow, fast = head, head.next;
        while fast:
            if slow.val != fast.val:
                slow.next = fast
                slow = fast
            fast = fast.next
        slow.next = None
        return head
```