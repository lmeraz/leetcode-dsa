# Stacks
Stack - an ordered collection of elements where elements are added and removed from the same end

Stacks: LIFO Last In First Out

pushing instert to tacks
poppiing removes from a stack
peeking looks at the element at the top of the stack
push/pop/random access o1 on search

recusrion uses a stack of function calls
tehtop of stack is calle the active call
return steatment pipsthe current call off the stack

# queues

While a stack followed a LIFO pattern, a queue follows FIFO (first in first out).
 In a queue, elements are added and removed from opposite sides
 An example of a queue in the physical world is a line at a fast food restaurant
 Adding to a queue is called enqueue and deletions are called dequeue
 One way to implement an efficient queue is by using a doubly linked lis

 There is also a data structure called a deque, short for double-ended queue, and pronounced "deck". In a deque, you can add or delete elements from both ends. A normal queue designates adding to one end and deleting to another end.

 #
 monotonic
 A monotonic stack or queue is one whose elements are always sorted. 

 ```
 Given an integer array nums

stack = []
for num in nums:
    while stack.length > 0 AND stack.top >= num:
        stack.pop()
    // Between the above and below lines, do some logic depending on the problem
    stack.push(num)
```

Monotonic stacks and queues are useful in problems that, for each element, involves finding the "next" element based on some criteria, for example, the next greater element.



We use a monotonic decreasing deque, which implies that the first element is the maximum.
Once the maximum element is too far to stay in the window we remove it from the deque, and the next greatest element moves to position 0.
To maintain the decreasing order, we remove elements from the deque that are smaller than the elements being added.
