# Assignment 12
## Part 1
### Identify the base case in given code
```
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
