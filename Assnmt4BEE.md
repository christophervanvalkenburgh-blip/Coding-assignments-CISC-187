# Assignment 4b
## Part A, 1-4
The code for selecting the appropirate category is the same in both sets of codes for part A and B, but in part A the list is generated in the program and then shuffled randomly. In part B, the user enters the elements and we only output either worst or average case, absorbing the nearly sorted into average. 
```C++
#include <iostream>
#include <vector>
#include <algorithm>
#include <random>
using namespace std;

//implementation of the selection sort
void selectionSort(vector<int> &arr) {
    int n = arr.size();

    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;

        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}

//implementation of insertion sort
void insertionSort(vector<int> &arr) {
    int n = arr.size();

    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = key;
    }
}

//verify which sort category, avg, almost, reverse
string analyzeOrder(vector<int>& arr) {
    int outOrder = 0;

    for (int i = 0; i <arr.size() - 1; i++) {
        if (arr[i] > arr[i + 1]) {
            outOrder++;
        }
    }
    //return category based on number of out of order pairs
    if (outOrder <= 5) {
        return "Almost Sorted";
    }
    else if (outOrder >=45) {
        return "Reverse Sorted";
    }
    else {
        return "Average";
    }
}


int main() {
    //new vector of 50 elements
    vector<int> arr(50);

    //fill elements of the vector with numbers 1-50
    for (int i =0; i < 50; i++) {
        arr[i] = i +1;
    }

    //Shuffle items in vector to set up test
    random_device rd;
    mt19937 g(rd());
    shuffle(arr.begin(), arr.end(), g);

    //call ordering function, return which category of sort
    string category = analyzeOrder(arr);

    cout << "Category: " << category << endl;

    //output the type of sort used
    if (category == "Almost Sorted") {
        cout << "Insertion Sort" << endl;
    insertionSort(arr);
    }
    else if (category == "Reverse Sorted") {
        cout << "Selection Sort" << endl;
        selectionSort(arr);
    }
    else if (category == "Average") {
        cout << "Insertion Sort" << endl;
        insertionSort(arr);
    }

    return 0;
}
```
## Part B
```C++
#include <iostream>
#include <vector>
using namespace std;

//verify which sort category, avg, almost, reverse
string analyzeOrder(vector<int>& arr) {
    int outOrder = 0;

    for (int i = 0; i <arr.size() - 1; i++) {
        if (arr[i] > arr[i + 1]) {
            outOrder++;
        }
    }
    if (outOrder <= 5) {
        return "Almost Sorted";
    }
    else if (outOrder >=45) {
        return "Reverse Sorted";
    }
    else {
        return "Average";
    }
}

int main() {
    vector<int> arr(50);
    //have user enter 50 ints
    cout << "Enter 50 integers!" << endl;
    for (int i = 0; i < 50; i++) {
        cin >> arr[i];
    }
    //call analyzeOrder fuction to determin category
    string category = analyzeOrder(arr);
    //output category
    if (category == "Reverse Sorted") {
        cout << "Worst Case" << endl;
    }
    else {
        cout << "Average Case" << endl;
    }

    return 0;
}
```
## Part C
The thresholds I chose for my assumption: We are doing comparisons with elements in the array, using arr[i] > arr[i+1]. Each of these is a pair out of order. If my out of order pairs is less than or equal to 5, I call that almost sorted. With greater than or equal to 45, I call that reverse sorted and anything between as an average case. The reasoning behind this is that the insertion sort is extremely good at nearly sorted arrays, with a best case of O(N). The selection sort is always O(N^2). The input order impacts the time complexity of the insertion sort but no the selection sort. So for our average case we are going to select insertion sort since it is still typically faster, reverse for selection and almost will be insertion. 
