# Assignment 12
## Part 1
### Identify the base case in given code
``` Python
return if low > high
```
## Part 2
### Predict what will happen when we run factorial(10) with given functiuon
The function will never reach n == 1. Subtracting 2 each time results in us reaching n == 0, and then continuing into the negative, causing the recursion to run infinitely until a stack overflow. This happens because the base case only handles n == 1, but starting at factorial(10) will skip it. 
## Part 3
### Add base case to fix given code
``` C++
int sum(int low, int high) {
  if (low == high) { //this was the missing base case
    return low;
  }

  return high + sum(low, high - 1);
}
```
## Part 4
### Write a recursive function that prints all the numbers (and just numbers).
``` C++
#include <iostream>
#include <string>
using namespace std;

/* function to print numbers from the nested array string. Index is passed by reference so
 * recursive calls keep track of the same position in the string */
void printNumbers(const string& array, int& index) {
    while (index < array.length()) { // keep scanning the string while index is still in the string
        if (isdigit(array[index])) { // check current character at index for digits
            // print every digit in the current nubmer until non digit reached
            while (index < array.length() && isdigit(array[index])) {
                cout << array[index];
                index++;
            }
            cout << endl;
        }
        /* if an opening bracket is found, new nested array -> increment index to move past it,
         * then call the printNumbers function to handle the new array */
        else if (array[index] == '[') {
            index++;
            printNumbers(array, index);
        }
        /* closing bracket shows nested array is done, increment index to move past it, return to
        previous recursive level */
        else if (array[index] == ']') {
            index++;
            return;
        }
        //skip past any spaces, new lines, commas, etc
        else {
            index++;
        }
    }
}

int main() {
    // store given nested array as a string
    string array =
        "[1,"
        "2,"
        "3,"
        "[4,5,6],"
        "7,"
        "[8,"
            "[9,10,11,"
                "[12,13,14]"
            "]"
        "],"
        "[15,16,17,18,19,"
            "[20,21,22,"
                "[23,24,25,"
                    "[26,27,29]"
                "],30,31"
            "],32"
        "],33]";

    int index = 0;
    printNumbers(array, index); 

    return 0;
}
```
