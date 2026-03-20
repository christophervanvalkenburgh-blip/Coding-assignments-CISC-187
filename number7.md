# Linked lists
Included in the second half of my main are a series of tests to ensure my program is working correctly. Can swap commented mains in order to see program output normally and test if desired. 
## Main.cpp
```
#include "stack.h"

int main()
{
    // Part 9: Driver Program

    Stack s; // create stack

    // push values
    s.push(10);
    s.push(20);
    s.push(30);
    s.push(40);

    // display full stack
    s.display();

    cout << endl;

    // remove top element (40)
    s.pop();

    // print new top
    cout << "Top element: " << s.peek() << endl;

    cout << endl;

    // display updated stack
    s.display();

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
//     // Normal pushes
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

    // new node points to old top
    newNode->next = top;

    // update top to new node
    top = newNode;
}

// Part 5 & Part 10: Implement pop() - check if empty, store current top, move top down, delete old node
void Stack::pop()
{
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

    return top->data;
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

    // use temp pointer so top doesn't get messed up
    Node* current = top;

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

    // new node points to old top
    newNode->next = top;

    // update top to new node
    top = newNode;
}

// Part 5: Implement pop() - check if empty, store current top, move top down, delete old node
void Stack::pop()
{
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

    return top->data;
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

    // use temp pointer so top doesn't get messed up
    Node* current = top;

    // move through entire stack
    while (current != nullptr)
    {
        cout << current->data << endl;
        current = current->next;
    }
}
```
