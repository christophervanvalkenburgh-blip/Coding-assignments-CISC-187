# Assignment 6
## Using Figure 17 as a model, in the book Data Structures in C++, illustrate the result of each operation in the sequence PUSH(S,4), PUSH(S,1), PUSH(S,3), POP(S), PUSH(S,8), and POP(S) on an initially empty stack S stored in array S[1..6]. 
[Part 1](part%201.png)
## Using Figure 18 as a model, in the book Data Structures in C++, illustrate the result of each operation in the sequence ENQUEUE(Q,4), ENQUEUE(Q,1), ENQUEUE(Q,3), DEQUEUE(Q), ENQUEUE(Q,8), and DEQUEUE(Q) on an initially empty queue Q stored in array Q[1..6].
[Part 2](part%202.png)
## Rewrite ENQUEUE and DEQUEUE to detect underflow and overflow of a queue. 
Enqueue: 
```
if ( (Q.tail == Q.length and Q.head == 1) or (Q.tail + 1 == Q.head) )
    report "Overflow"
else
    Q[Q.tail] = x
    if Q.tail == Q.length
        Q.tail = 1
    else
        Q.tail = Q.tail + 1
```
Dequeue
```
if Q.head == Q.tail
    report "Underflow"
else
    x = Q[Q.head]

    if Q.head == Q.length
        Q.head = 1
    else
        Q.head = Q.head + 1

    return x
```
## A stack allows insertion and deletion of elements at only end, and a queue allows insertion at one end and deletion at the other end, a deque (double-ended queue) allows insertion and deletion at both ends. Write four O(1)-time procedures to insert elements into and delete elements from both ends of a deque implemented by an array. 
Insert front & back
```
Insfront(D, x)
  D.head = (D.head - 1) mod D.length
  D[D.head] = x
```
```
Insback(D, x)
  D[D.tail] = x
  D.tail = (D.tail + 1) mod D.length
```
Delete front & back
```
Deletefront(D)
  x = D[D.head]
  D.head = (D.head + 1) mod D.length
  return x
```
```
Deleteback(D)
  D.tail = (D.tail - 1) mod D.length
  x = D[D.tail]
  return x
```
