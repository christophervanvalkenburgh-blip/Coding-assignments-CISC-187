# Assignment 2
## How many steps would it take to perform a linear search for the number 8 in the ordered array, [2, 4, 6, 8, 10, 12, 13]?
In a linear search, you check elements from left to right until you get a match. So this would take 4 steps.
## How many steps would binary search take for the previous example?
Binary search works by starting at the middle value, and comparing whether it is greater than or less than, and then cutting the half off that isn't applicable. In this example, the middle is 8 and that is our value, so it takes 1 step. 
## What is the maximum number of steps it would take to perform a binary search on an array of size 100,000?
The number of steps a binary search takes is the log2(N), rounded up. So in this case it would be 16.61 rounded to 17. 
## Code for part 4
```C++
#include <iostream>
using namespace std;

int linearSearch(int arr[], int size, int key, int &steps) { // Linear Search method
    steps = 0; //initialize steps to zero

    for (int i = 0; i < size; i++) {
        steps++;  // count number of steps for comparison
        if (arr[i] == key) { //if found match, return
            return i;
        }
    }

    return -1;  // no match found
}

int binarySearch(int arr[], int size, int key, int &steps) { // Binary Search method
    int left = 0; //initialize left to beginning
    int right = size - 1; //initialize right to end
    steps = 0; //initialize steps to zero

    while (left <= right) { //while loop to search for a match utilizing binary search
        int mid = left + (right - left) / 2;
        steps++;  // count comparison

        if (arr[mid] == key) {
            return mid;  // found value, return
        }
        else if (arr[mid] < key) {
            left = mid + 1; //value is above midpoint, set left to one above mid
        }
        else {
            right = mid - 1; //value is below midpoint, set right to one below mid
        }
    }

    return -1;  // value not found, return
}

int main() {

    const int SIZE = 100000; //declare and initialize constant value for array size
    int arr[SIZE]; //initialize array to size of constant value

    for (int i = 0; i < SIZE; i++) { // Fill array with values 1 to 100000
        arr[i] = i + 1;  // 1 to 100000
    }

    int key = 100000;  // worst-case for linear search

    int linearSteps; //declare linear and binary step counts
    int binarySteps;

    linearSearch(arr, SIZE, key, linearSteps); //call linear method
    binarySearch(arr, SIZE, key, binarySteps); //call binary method

    cout << "Linear Search Steps: " << linearSteps << endl; //output number of linear steps
    cout << "Binary Search Steps: " << binarySteps << endl; //output nubmer of binary steps

    return 0;
}
```
### Explanation
In the above program, the resulted count for linear search for a worst case scenario was 100000 steps, and for the binary search it was 17 steps. This is a clear illustration of the advantage of binary search over linear search. Utilizing linear search examines elements sequentially from the beginning of the array until the value is found. This results in the O(N) notation where N represents the number of elements in the array. In the worst case scenario, either the element is last or it is not included in the array at all, which requires examining every single element. 
Binary search, on the other hand, eliminates half of the remaining elements after each step, drammatically cutting down on search time. After 1 step, N/2 elements remain, after 4 it's N/4 and so on. So after K steps of N/2^K -> we solve for K which gives us log2(N). The number of comparisons grows logrithmically, so O(log N). 
## Part 5
We can write code that searches through a list randomly each time by generating a vector of data and indexes, shuffling the index vector randomly, and then using this to compare against our data vector. 
### Pseudocode for part 5
```Pseudocaode
n <- 100000 //total number of elements
comparison <- 0 //couting elements checked

indices <- new array size of n //create a list of the indices
for i from 0 to n-1
indices[i] <- 1 //store each index to the indices array

for i from n-1 to 1
j <-random integer in [0,i]
swap (indices[i], indices[j]) //shuffle the indices randomly

for t from 0 to n-1
indx <- indices[t] //get next random index
comparisons <- comparisons + 1 //count nuber of comparisons

if A[indx] == key
return (indx, comparisons) //key is found, return it's position and number of comparisons

return (-1, comparisons) //return if key not found, number of comparisons
```
Best case scenario is O(N) where O(1). If the first value chosen is our key, it takes one step. On average, we expect to find our value at N/2, where the value is in the middle. This scales proportionally to the size of the array so our average time is O(N). For a worse case, it is also O(N) where n is the total number of elements in the array. Big-O measures growth rate, not exact operational count, so the constant of 1/2 is irrelevant.  
### Code for part 5
```C++
#include <vector>
#include <random>
#include <iostream>

using namespace std;

int randomizedSearchNoRepetition(vector<int> data, int key)
{
    int n = data.size(); //total number of elements in vector
    int comparisons = 0; //initialize comparisons to zero

    vector<int> indices(n);
    for (int i = 0; i < n; i++) { //initialize vector, fill with values
        indices[i] = i;
    }

    random_device rd; //declare random number generator for shuffling random indexes

    for (int i = n - 1; i > 0; i--) {
        int j = rd() % (i + 1);  // assign j with random index

        int temp = indices[i]; //store i in temp value so it doesn't get overwritten, swap with j
        indices[i] = indices[j];
        indices[j] = temp;
    }

    for (int i = 0; i < n; i++) { //for loop which loops through the vector to find key
        comparisons++;

        if (data[indices[i]] == key) { //compare data at the index of randomized indexes with key value
            cout << "Found at index: " << indices[i] << endl; //output index found
            cout << "Comparisons: " << comparisons << endl; //output total number of comparisons
            return indices[i];
        }
    }

    cout << "Not found." << endl; //output if not found in vector
    cout << "Comparisons: " << comparisons << endl; //output comparison total for not found
    return -1;
}

int main()
{
    const int N = 100000; //delclare and initialize constant N for vector size

    vector<int> data; //declare vector data and fill with unique values
    for (int i = 1; i <= N; i++) {
        data.push_back(i);
    }

    int key; //declare key and initialize to user-input value
    cout << "Enter key: ";
    cin >> key;

    randomizedSearchNoRepetition(data, key); //call search method

    return 0;
}
```
### Comparisons
Randomized search and linear search both have the same best case time complexity of O(1) and average and worst case time complexity of O(N) since in both algorithms, the program may have to search every single element, or it may be the first element checked. The only difference between randomized and linear search is that one examines a predetermined order and the other just shuffles into a different order, but both have an equally likely chance of best and worst case scenarios. However, the additional randomization step has a complexity of O(N) as well, potentially doubling the time it takes to search. Now for binary, the data must be sorted initially, which also requires time complexity. Since binary has a simpler actual search complexity, with a best case of O(1) and a worst case of O(logN) which is a significant reduction in time complexity. Because each step eliminates half of the remaining elements to be checked, it performs dramatically fewer comparisons than either linear or randomized search. Linear search is preferred for small data sets where order isn't important because the search is so fast with a short list. Randomized search may be useful in situations where bias needs to be removed or an unpredictable order is desired, such as for randomized sampling. Binary search is preferred for long stored data sets where time to search is now an important factor. 
## Video
https://youtu.be/AQBOokSdszw
