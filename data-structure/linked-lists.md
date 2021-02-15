linkedlist 基础知识

LinkedList 种类:
1. doubly LinkedList
2. singly LinkedList

LinkedList 基本操作：
1. dummy node
2. middle node
3. reverse
4. hasCycle

java
```
class DoublyLinkedList {
  Node head = new Node(-1, -1);
  Node tail = new Node(-1, -1);

  public DoublyLinkedList(int value) {
    head.next = tail;
    tail.prev = head;
  }

  public void remove(Node node) {
    node.next.prev = node.prev;
    node.prev.next = node.next;
  }

  private class Node {
    int valule;
    Node next;
    Node prev;
    public Node(int value) {
      this.value = value;
    }
  }
}
```
