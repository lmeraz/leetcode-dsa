# Linked Lists
## A ListNode Class
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
    
one = ListNode(1)
two = ListNode(2)
three = ListNode(3)
one.next = two
two.next = three
head = one

print(head.val)
print(head.next.val)
print(head.next.next.val)
```

Assignment (=)
When you assign a pointer to an existing linked list node, the pointer refers to the object in memory. After these lines of code, ptr still refers to the original head node, even though the head variable changed. This is the first important concept: variables remain at nodes unless they are modified directly (ptr = something is the only way to modify ptr).

Chaining .next

If you have multiple .next, for example head.next.next, everything before the final .next refers to one node. For example, given a linked list 1 -> 2 -> 3, if you have head pointing at the first node, and you do head.next.next, you are actually referring to 2.next, because head.next is the 2. We'll soon see that this is a very useful technique.

traversal

Iterating forward through a linked list can be done with a simple loop. This is the usual code that you will use to do so: as an example let's get the sum of all values from an integer linked list:
```python
def get_sum(head):
    ans = 0
    while head:
        ans += head.val
        head = head.next
    
    return ans
```

Moving to head.next is the equivalent of iterating to the next element in an array. Traversal can also be done recursively:
```python
def get_sum(head):
    if not head:
        return 0
    
    return head.val + get_sum(head.next)
```

Types of linked lists
singly linked lists

This is the most common type of linked list and the one that is given in the code above. In a singly linked list, each node only has a pointer to the next node. This means you can only move forward in the list when iterating. The pointer used to reference the next node is usually called next.

Let's say you want to add an element to a linked list so that it becomes the element at position i. To do this, you need to have a pointer to the element currently at position i - 1. The next element (currently at position i), call it x, will be pushed to the element at position i + 1 after the insertion. This means that x should become the next node to the one being added, and the node being added should become the next node to the one currently at i - 1. Here's some code and images demonstrating:
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

# Let prev_node be the node at position i - 1
def add_node(prev_node, node_to_add):
    node_to_add.next = prev_node.next
    prev_node.next = node_to_add
```

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

# Let prev_node be the node at position i - 1
def delete_node(prev_node):
    prev_node.next = prev_node.next.next
```

Doubly LInked list
Doubly linked list

A doubly linked list is like a singly linked list, but each node also contains a pointer to the previous node. This pointer is usually called prev, and it allows iteration in both directions.

In a singly linked list, we needed a reference to the node at i - 1 if we wanted to add or remove at i. This is because we needed to perform operations on the prevNode. With a doubly linked list, we only need a reference to the node at i. This is because we can simply reference the prev pointer of that node to get the node at i - 1, and then do the exact same operations as above.

With a doubly linked list, we need to do extra work to also update the prev pointers.
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
        self.prev = None

# Let node be the node at position i
def add_node(node, node_to_add):
    prev_node = node.prev
    node_to_add.next = node
    node_to_add.prev = prev_node
    prev_node.next = node_to_add
    node.prev = node_to_add

# Let node be the node at position i
def delete_node(node):
    prev_node = node.prev
    next_node = node.next
    prev_node.next = next_node
    next_node.prev = prev_node
```

Linked lists with sentinel nodes

We call the start of a linked list the head and the end of a linked list the tail.
Sentinel nodes sit at the start and end of linked lists and are used to make operations and the code needed to execute those operations cleaner. The idea is that, even when there are no nodes in a linked list, you still keep pointers to a head and tail. The real head of the linked list is head.next and the real tail is tail.prev. The sentinel nodes themselves are not part of our linked list.

The previous code we looked at is prone to errors. For example, if we are trying to delete the last node in the list, then nextNode will be null, and trying to access nextNode.next would result in an error. With sentinel nodes, we don't need to worry about this scenario because the last node's next points to the sentinel tail.
The sentinel nodes also allow us to easily add and remove from the front or back of the linked list. Recall that addition and removal is only 
O
(
1
)
O(1) if we have a reference to the node at the position we are performing the operation on. With the sentinel tail node, we can perform operations at the end of the list in 
O
(
1
)
O(1).
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
        self.prev = None

def add_to_end(node_to_add):
    node_to_add.next = tail
    node_to_add.prev = tail.prev
    tail.prev.next = node_to_add
    tail.prev = node_to_add

def remove_from_end():
    if head.next == tail:
        return

    node_to_remove = tail.prev
    node_to_remove.prev.next = tail
    tail.prev = node_to_remove.prev

def add_to_start(node_to_add):
    node_to_add.prev = head
    node_to_add.next = head.next
    head.next.prev = node_to_add
    head.next = node_to_add

def remove_from_start():
    if head.next == tail:
        return
    
    node_to_remove = head.next
    node_to_remove.next.prev = head
    head.next = node_to_remove.next

head = ListNode(None)
tail = ListNode(None)
head.next = tail
tail.prev = head
```

Dummy pointers
Dummy pointers

As mentioned earlier, we usually want to keep a reference to the head to ensure we can always access any element. Sometimes, it's better to traverse using a "dummy" pointer and to keep head at the head.

```python
def get_sum(head):
    ans = 0
    dummy = head
    while dummy:
        ans += dummy.val
        dummy = dummy.next
    
    # same as before, but we still have a pointer at the head
    return ans
```

Using the dummy pointer allows us to traverse the linked list without losing a reference to the head.

# Fast and Slow Pointers
```
// head is the head node of a linked list
function fn(head):
    slow = head
    fast = head

    while fast and fast.next:
        Do something here
        slow = slow.next
        fast = fast.next.next
```

The reason we need the while condition to also check for fast.next is because if fast is at the final node, then fast.next is null, and trying to access fast.next.next would result in an error (you would be doing null.next).

```python3
def get_middle(head):
    slow = head
    fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    return slow.val
```