# Assignment 3
## Use Big O Notation to describe the time complexity of an algorithm that takes 4N+16 steps.
In big O notation, we ignore constants and low order terms, so O(N)
## Use Big O Notation to describe the time complexity of an algorithm that takes 2N^2. 
In big O notation, we ignore constants, so O(N^2)
## Use Big O Notation to describe the time complexity of the function, which returns the sum of all numbers of an array after the numbers have been doubled.
This function takes a time complexity of O(N) to double the numbers, and O(N) to calculate the sum. That's O(N) + O(N) = O(2N). Drop the constant, so O(N).
## Use Big O Notation to describe the time complexity of the function, which accepts an array of strings and prints each string in multiple cases.
This code performs 3 linear actions to the array, all with time complexity of O(N). O(3N) = O(N).
## The next function iterates over an array of numbers, and for each number whose index is even, it prints the sum of that number plus every number in the array. What is this function’s efficiency in terms of Big O Notation?
The outer loop runs N times. The inner loop runs with every even index, so N/2 times. Multiply, and you get N^2/2. So our time complexity is O(N^2). 
