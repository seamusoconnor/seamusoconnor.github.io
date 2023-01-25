---
title: '[ C ] Bubble Sort'
date: 2023-01-25 01:00:00 +0100
categories: [C]
tags: [software, development, sorting, algorithms]
---


## Background

As part of my C studies, I'm writing a sorting algorithm, namely Bubble Sort.

It's not the fastest sorting algorithm for large data sets as it needs to pass-through the array n number of times for n number of elements in the array. 3-times for a 3-element array as can be seen below.  

Time complexity is: O(N^2)  
Space Complexity is O(1)  


Conceptually, Bubble Sort is an easy one to describe.

Take an array of three integers:


Array: ```{2,4,1}```

Iterate through the array 3 ( the number of elements in the array ) times.
<br><br><br><br>
1. First time through the array

    + is the 1st element ```(2)```  greater than the 2nd element ```(4)```  ?  
      + no -> leave them  

    Array: ```{2,4,1}```  

    + is the 2nd element ```(4)```  greater than the 3rd element ```(1)```  ?  
      + yes -> swap them

    Array: ```{2,1,4}```  

<br><br>
No point checking the 3rd (last element) as there's no 4th element to compare it with.  
We've completed our first pass through the array and have an array that looks like this: ```{2,1,4}```  

Let's go through the next pass-through:
<br><br><br><br>

2. Second time through the array

    + is the 1st element ```(2)```  greater than the 2nd element ```(1)```  ?  
      + yes -> swap them  

    Array: ```{1,2,4}```  

    + is the 2nd element ```(2)```  greater than the 3rd element ```(4)```  ?
        + no -> leave them  
  
    Array: ```{1,2,4}```  

<br><br>
No point checking the 3rd (last element) as there's no 4th element to compare it with.  
We've completed our second pass through the array and have an array that looks like this: ```{1,2,4}``` 


Let's go through the next, third ( and last ) pass-through:
<br><br><br><br>

3. Third time through the array

    + is the 1st element ```(1)```  greater than the 2nd element ```(2)```  ?  
        + no -> leave them

    + is the 2nd element ```(2)```  greater than the 3rd element ```(4)```  ?
        + no -> leave them

<br><br>
No point checking the 3rd (last element) as there's no 4th element to compare it with.  
We've completed our third pass through the array and have an array that looks like this: ```{1,2,4}``` 
<br><br><br>

We have sorted our array - In this use-case, we had a sorted array at the end of the 2nd pass but that depends on the initial state of the array. Algorithms are written for generic use-cases.  
<br><br>
So - How does this look in C ? 
<br><br>



## Source Code
```C
# include <stdio.h>

int main ( void )
{

    int arr[10] = { 2, 8, 3, 6, 4, 5, 1, 7, 9, 10 }; // our unsorted array

    // number of elements in the array
    int size_of_array = (sizeof(arr) / sizeof(arr[0]));

    // number of passes through the array = number of elements in the array
    for (int num_passes = 0; num_passes < size_of_array; num_passes++)
    {

        // checks and swaps each element, when it does a pass through the array (except the last element)
        for (int i = 0; i < size_of_array -1 ; i++ )
            {

                int temp = arr[i]; // assign the earlier element in a temporary variable
                if (arr[i] > arr[i + 1]) // if the earlier element is greater than the later element
                {

                    arr[i] = arr[i + 1]; // assign the later element to the earlier one
                    arr[i + 1] = temp; // assign the temp value to the later element
                }
            }
        }

    // This prints out the sorted array by iterating through the elements
    // and printing them one-at-a-time
    // prints 1 2 3 4 5 6 7 8 9 10 
    printf("The sorted Array is: ");
    for (int i = 0; i < size_of_array ; i++ )
        {
            printf("%d ", arr[i]);
        }
        return 0;
}

```


## Output

```
The sorted Array is: 1 2 3 4 5 6 7 8 9 10 
```


‌