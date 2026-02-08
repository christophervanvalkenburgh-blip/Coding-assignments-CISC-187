# Assignment 1
## Code for part 1
```C++
#include <iostream>
using namespace std;

int main() {
    int arr[100]; //create array of 100 int elements

    return 0;
  }
```
## Code for part 2
```C++
#include <iostream>
using namespace std;

int main() {
    int arr[100]; // create array of 100 int elements

    cout << "Size of an element: " << sizeof(arr[0]) << " bytes" << endl; //output size of array in bytes

    return 0;
  }
```
## Part 3

### Reading
Reading a value at any specific index in the array takes a single step.
### Searching for a value not contained in the array
Searching for a value not contained in the array requires the program to check every single value, resulting in 100 steps. 
### Insertion at the beginning of the array
Due to arrays having a fixed order, inserting an element at the beginning requires shifting all other elements resulting in 100 steps.
### Insertion at the end of the array
Inserting at the end of an array does not require shifting and therefore takes a single step.
### Deletion at the beginning
Deleting an element at the beginning of an array leaves a gap, requiring 99 steps to rectify, or 100 including the deletion.

## Part 4
In order to find all instances of a given value in an array, the program would have to look at every single element. The number of steps N is equal to the number of elements, N in the array.

## Code for part 5
```C++
#include <iostream>
using namespace std;

int main() {
    int arr[100]; // new array of 100 elements
    
    cout << "arr: " << arr << endl; //output memory address of array

    return 0;
}
```
## Video link
https://youtu.be/H0lJ557fKgk


