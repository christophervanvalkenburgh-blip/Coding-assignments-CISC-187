# Linked lists
Included below my main program is a commented-out test section I used to verify that the stack was working correctly, including underflow cases. You can swap in the commented text to test if needed.
## Main.cpp
```
#include "stack.h"

int main()
{
    // Part 9: Driver Program

    Stack s; // create stack

    s.push(10);
    s.push(20);
    s.push(30);
    s.push(40);
    
    s.display(); // display full stack

    cout << endl;

    s.pop(); // remove top element (40)

    cout << "Top element: " << s.peek() << endl;  // print new top

    cout << endl;

    
    s.display(); // display updated stack

    return 0;
}
// #include "stack.h"
//
// int main()
// {
//     Stack s;
//
//     // Test underflow on empty stack
//     cout << "Testing pop on empty stack:" << endl;
//     s.pop();
//
//     cout << "\nTesting peek on empty stack:" << endl;
//     cout << s.peek() << endl;
//
//     s.push(10);
//     s.push(20);
//     s.push(30);
//
//     cout << "\nAfter pushing 10, 20, 30:" << endl;
//     s.display();
//
//     // Pop everything
//     cout << "\nPopping all elements:" << endl;
//     s.pop();
//     s.pop();
//     s.pop();
//
//     cout << "\nStack should now be empty:" << endl;
//     s.display();
//
//     // Force underflow again
//     cout << "\nTrying to pop again (should underflow):" << endl;
//     s.pop();
//
//     // Mixed operations
//     cout << "\nMixed operations test:" << endl;
//     s.push(100);
//     s.push(200);
//     s.pop();
//     s.push(300);
//
//     s.display();
//
//     return 0;
// }
```
## Stack.cpp
```
#include "stack.h"

// Part 3: Implement the Constructor - initializes the stack as empty
Stack::Stack()
{
    top = nullptr;
}

// Part 4: Implement push() - create new node, point it to current top, update top
void Stack::push(int value)
{
    Node* newNode = new Node; // create node
    newNode->data = value;    // assign value

    newNode->next = top; // new node points to old top

    top = newNode; // update top to new node
}

// Part 5: implement pop() - remove top node
void Stack::pop()
{
    // Part 10: stack underflow
    if (isEmpty())
    {
        cout << "Stack Underflow" << endl;
        return;
    }

    Node* temp = top;    // store current top
    top = top->next;     // move top to next node
    delete temp;         // free memory
}

// Part 6: Implement peek() - returns value at top without removing it
int Stack::peek()
{
    if (isEmpty())
    {
        cout << "Stack is empty" << endl;
        return -1;
    }

    return top->data; //return value
}

// Part 7: Implement isEmpty() - returns true if stack is empty
bool Stack::isEmpty()
{
    return top == nullptr;
}

// Part 8: Implement display() - prints stack from top to bottom
void Stack::display()
{
    if (isEmpty())
    {
        cout << "Stack is empty" << endl;
        return;
    }

    cout << "Stack elements:" << endl;

    Node* current = top; // use temp pointer so top doesn't get messed up

    // move through entire stack
    while (current != nullptr)
    {
        cout << current->data << endl;
        current = current->next;
    }
}
```
## Stack.h
```
#ifndef STACK_H
#define STACK_H

#include <iostream>
using namespace std;

// Part 1: This struct represents a single node in the linked list
struct Node
{
    int data;
    Node* next;
};

// Part 2: Stack implemented using a linked list
class Stack
{
private:
    Node* top; // pointer to the top of the stack

public:
    Stack();           // constructor

    void push(int value);  // add element to top
    void pop();            // remove top element
    int peek();            // view top element
    bool isEmpty();        // check if empty
    void display();        // print stack
};

#endif
```
## Reflection Questions
[View Answers](https://github.com/christophervanvalkenburgh-blip/Coding-assignments-CISC-187/blob/main/READMElab7.md)
