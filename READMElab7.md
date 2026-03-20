# Assignment 7 readme
## Why is a linked list efficient for stack implementation?
It's efficient for a stack because we only add or remove elements from the top. Using a linked list, we can do this by just updating the one element at the top, not requiring the shifting of all elements as in an array, which keeps operations at O(1) complexity.
## What is the time complexity of push and pop operations?
Push and pop operations only involve updating pointers at the top of the stack so they both only have O(1) complexity.
## What happens if memory is not deallocated after pop?
THe most devastating thing that can happen to a program. A memory leak. The program keeps using more memory as it runs over time until it runs out. Donkey Kong on N64 famously had a memory leak which would crash the game if played for too long. I'm old enough to remember this. 
## Compare a stack implemented with an array versus a linked list.
A stack implemented with an array uses a fixed size. It can access with O(1) time complexity if you know the element by index, but it can run out of space due to an overflow. It does not require extra memory for pointers.
A linked list stack has a dynamic size and has no overflow (assuming infinite memory), but it does use extra memory for pointers and you must traverse to find an element. 
