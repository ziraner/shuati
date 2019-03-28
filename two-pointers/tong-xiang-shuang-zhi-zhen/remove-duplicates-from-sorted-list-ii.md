Remove Duplicates from Sorted List II

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

Example 1:
Input: 1->2->3->3->4->4->5
Output: 1->2->5

Example 2:
Input: 1->1->1->2->3
Output: 2->3

Idea:
跟1不同，需要构造一个dummy节点，而且需要另外一个循环判断挨着的两个点是相同的or not

Solution:
```
class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head
        dummy = ListNode(0)
        dummy.next = head
        slow, fast = dummy, head
        while fast and fast.next:
            if fast.val == fast.next.val:
                val = fast.val
                while fast and fast.val == val:
                    fast = fast.next
                slow.next = fast
            else:
                slow = slow.next
                fast = fast.next
        return dummy.next
```