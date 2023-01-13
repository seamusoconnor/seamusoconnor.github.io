---
title: '[ C ] Return Multiple Variables From a Function Using Pointers'
date: 2023-01-13 23:30:00 +0100
categories: [C]
tags: [software, mac, development, pointers, functions]
---


## Background

As part of my C studies, I'm writing a menu-driven program that calls certain functions based off the user inputs.
One of the concepts I've found difficult to master is pointers and how to use them.
C in the simplest understanding of it, does not return more than one value from a function.

Typically a function looks like this:

```C
int func1()
{
    return 5; // int defined must match the datatype being returned, in this case 5
}
```

Another:
```C
void func2()
{
    // nothing is returned here and this is enforced
}
```

Coming from python, it's been something that has taken a bit of getting used to, and for the most part, I've worked around this limitation by reducing the complexity of functions ( always a good idea ).
I have an assignment with certain constraints that, probably on purpose, force me to return two integers from a function.
Checking through stackoverflow I found two options.

1. using pointers - This is what I'll try here
2. using structs - Some other time

I played around with both of these for a couple of hours, and although I've worked with both a small amount, my main problem in building my knowledge is that the program I'm writing is about 80% done so making a lot of changes is starting to get confusing :-) 



I found an amazing Youtube Channel that has been helping me along my C journey and luckily enough, he was able to save me again with this <a href="https://www.youtube.com/watch?v=R8IogBSLXV0" target="_blank">video</a> . I wrote a small program based off my learning.


## Source Code

```c
#include <stdio.h>

// don't over-complicate things - build variables as normal and assign the pointer values at the end

// prototype with arguments that point to the variables
void func(int *area, int *perimeter);


int main ( void )
{

    int area_result = 0;
    int perimeter_result = 0;

    printf("output before function:\n area_result: %d\nperimeter_result: %d\n", area_result, perimeter_result);

    // pass the memory address of the variable 'area_result' and 'perimeter_result' into the function
    func(&area_result, &perimeter_result);

    printf("output after function:\narea_result: %d\nperimeter_result: %d\n", area_result, perimeter_result);

    return 0;
}

void func(int *area, int *perimeter)
{

    int x = 100;
    int y = 200;

    *area = x; // assign 100 to the area pointer
    *perimeter = y; // assign 200 to the perimeter pointer
}

```


## Output

```
output before function:
area_result: 0
perimeter_result: 0
output after function:
area_result: 100
perimeter_result: 200
```


## Reference:

Courses, P. (2021). How To ‘Return’ More Than One Value From A Function | C Programming Example. [online] www.youtube.com. Available at: https://www.youtube.com/watch?v=R8IogBSLXV0 [Accessed 13 Jan. 2023].
‌