# Assignment 13
## Task 1: Following is the 'Word Builder' algorithm. Describe its space complexity in terms of Big O.
O(N^2): This function creates and empty array "collection" and then uses two nested loops. The outer loop runs N times, the inner loop runs N times. The function doesn't push anything when i == j, but it does push a new combined word for every other pair. So for an array size N, it stores N * (N - 1). Big O ignores constants so we are left with N^2. 
## Task 2: Following is a function that reverses an array. Describe its space complexity in terms of Big O
O(N): This function creates a new array newArray, and then loops through the original array from the end to the beginning and pushes every element into newArray. If the input array has N elements, the new array also does. It's just storing a second copy of the array in reverse, and the memory size grows directly with input so the space complexity is O(N). 
## Task 3: Create a new function to reverse an array that takes up just O(1) extra space.
``` C++
function reverseInPlace(array) {
    let left = 0;
    let right = array.length - 1;

    // keep swapping values until the two sides meet in the middle
    while (left < right) {
        let temp = array[left]; 
        array[left] = array[right]; 
        array[right] = temp; 

        left++; 
        right--; 
    }

    return array;
}
```
## Task 4: Fill in the table that follows to describe the efficiency of these three versions in terms of both time and space
| Version | Time complexity | Space complexity |
|---|---|---|
| Version #1 | O(N) | O(N) |
| Version #2 | O(N) | O(1) |
| Version #3 | O(N) | O(N) |
