# Assignment 4a
## 1. Prove that, under the average-case scenario, the insertion sort has a time complexity of O(N^2). Draw a clear figure and show all the operations clearly.
For an average-case scenario, we expect our element to have to move on average, about half of the i elements to the left and we expect them to be about half sorted already. Since big o drops constants, we are left with i number of comparisons. So we run from i = 1 to N - 1. So this is a summation of n to n - 1 x 1/2 X 1/2, or n(n-1)/4. We dropped the constant and the N^2 dominates, so we are left with O(N^2).   
I spent over an hour trying to figure out how to put this in a visual:   
[CISC187.pdf](https://github.com/user-attachments/files/25669856/CISC187.pdf)  
I came back to this later and watched some youtube videos. I have modified my diagram to show the steps more clearly than I originally show with a better proof and additional video. I also updated my explanation for the proof above and go over that in the video.   
[Sort.pdf](https://github.com/user-attachments/files/25676484/Sort.pdf)
## 2.
Worst case assumes that for ever i we have i number of comparisons and i number of shifts. So we have for each element 2i number of operations. 
### a) Starting at i = 1. 
i = 1, 2(1) = 2  
i = 2, 2(2) = 4  
i = 3, 2(3) = 6  
i = 4, 2(4) = 8  
Total operations equal 20.
### bi) Starting at i = 2
i = 2, 2(2) = 4  
i = 3, 2(3) = 6  
i = 4, 2(4) = 8  
Total operations equal 18
### bii) Starting at i = 3
i = 3, 2(3) = 6  
i = 4, 2(4) = 8  
Total operations equal 14
### c) For (b), does the algorithm still sort the entire array? Explain.
No, it does not. Insertion sort assumes that the elements prior to the i we start at are already sorted. We ignored the lower elements in summing our total operations. So two things can happen. Either they were sorted, in which case our sorting works fine, or they are not, in which case we will end up with everything sorted from our selected element forward. 
## 3.
### a) What is this function’s time complexity regarding Big O Notation?
This is no different than a linear sort. It has to check every single element, since the loop runs from i = 0 to 1 less than the length. The time complexity is O(N). 
### b) Then, modify the code to improve the algorithm’s efficiency for best- and average-case scenarios.
We can improve this code by adding a return if the X is found and removing the foundx boolean: 
```
function containsX(string) {
	for(let i = 0; i < string.length; i++) { 
		if (string[i] === "X") {
			return true; 
		}
	}
	return false; 
}
```
## Video
https://youtu.be/oowI49ZP7ks
## Video with updated diagram explanation
