---
title: C Hello World
date: 2022-12-14 08:00:00 +0100
categories: [C]
tags: [software, mac, development, hello world]
---


## Background

I am learning C as part of my Software Engineering studies. As is tradition, here is my first program with a break-down of its elements.






## The Source Code

```c

// This is a single-line comment

/*
This is a
multi-line comment
*/

#include <stdio.h> // header file

int main ( void ) // function named 'main' with no input which returns an integer value
{
    printf("Hello World!\n");// library function that prints to the screen
    return 0; // return 0 for success
}

```






Commenting in C can be done with
```c
// single-line comment goes here
```

or 

```c
 /*
 Multi-line
 goes here
 */
 ```



## Header Files

``` #include <stdio.h> ``` Header files are libraries, functions, variables or other data that can be imported into the C program using the C preprocessor     


## What is the C preprocessor ?
The C preprocessor executes before a program is compiled. In this case, the preprocessor includes other files into the file being compiled.

<br><br>
``` <stdio.h> ``` is a C library that provides file operation support and in the case of our program, input/output capabilities.

<br>

``` int main ( void ) ``` is the function declaration. In this case ```int``` indicates the datatype that will be returned from the function. ```main``` indicates the name of the function and ```( void )``` indicates that there are no input arguments to the function.

<br><br>
```printf``` is a function that prints formatted output to ```stdout```. In this case, it prints ```Hello World!``` to the users screen.

<br><br>
As for the ```\n``` character, ``` \ ``` is an escape character, to allow special characters to be represented. In this case ``` \n ``` is for **newline**. Some others are [here](#escape-characters) (Geeksforgeeks, 2017).

<br><br>
``` return 0; ``` is the integer value returned. ```0``` is for a successful execution / normal exit of the function. Other values indicate that an error occurred. The  ```main()``` function returns and implicit ```0``` if not ```return``` statement is used. Some other exit codes can be seen [here](#exit-codes) (Geeksforgeeks, 2020).

<br><br><br><br>
### Appendix:
<br><br>

### Escape Characters

<br>

| Escape Sequence | Meaning	| Explanation |
|-----------------|---------|-------------|
| \a	| Alarm or Beep	| A beep sound is generated |
| \b	| Backspace	| 	Backspace |
| \f	| Form Feed	| 	Form Feed page break(Return) |
| \n	| New Line	| 	Shift the cursor control to the new line |
| \r	| Carriage Return	|   Shift the cursor to the beginning of the current line |
| \t	| Tab (Horizontal)	| 	Shift the cursor to a couple of spaces(Eight blank spaces) to the right in the same line |
| \v	| Vertical Tab	| 	Vertical Tab |
| ```\\```	| Backslash	| 	Print the backslash character |
| \’	| Single Quote	| 	Display the single-quotation mark. |
| \”	| Double Quote	| 	Print the double-quotation mark |
| \?	| Question Mark	| 	Display the question mark |
| \nnn	| octal number	| 	Represent an octal number |
| \xhh	| hexadecimal number	| 	Represent a hexadecimal number |
| \0	| Null	| 	Termination of the string |

<br><br>
### Exit codes

<br>

- **exit(1):** It indicates abnormal termination of a program perhaps as a result a minor problem in the code.
- **exit(2):** It is similar to [exit(1)](https://www.geeksforgeeks.org/exit0-vs-exit1-in-c-c-with-examples/) but is displayed when the error occurred is a major one. This statement is rarely seen.
- **exit(127):** It indicates command not found.
- **exit(132):** It indicates that a program was aborted (received **[SIGILL](https://www.geeksforgeeks.org/program-error-signals/)**), perhaps as a result of illegal instruction or that the binary is probably corrupt.
- **exit(133):** It indicates that a program was aborted (received **[SIGTRAP](https://www.geeksforgeeks.org/signals-c-language/)**), perhaps as a result of dividing an integer by zero.
- **exit(134):** It indicates that a program was aborted (received **[SIGABRT](https://www.geeksforgeeks.org/program-error-signals/)**), perhaps as a result of a failed assertion.
- **exit(136):** It indicates that a program was aborted (received **[SIGFPE](https://www.geeksforgeeks.org/program-error-signals/)**), perhaps as a result of floating point exception or integer overflow.
- **exit(137):** It indicates that a program took up too much memory.
- **exit(138):** It indicates that a program was aborted (received **[SIGBUS](https://www.geeksforgeeks.org/segmentation-fault-sigsegv-vs-bus-error-sigbus/)**), perhaps as a result of unaligned memory access.
- **exit(139):** It indicates **Segmentation Fault** which means that the program was trying to access a memory location not allocated to it. This mostly occurs while using pointers or trying to
access an out-of-bounds array index.
- **exit(158/152):** It indicates that a program was aborted (received **SIGXCPU**), perhaps as a result of CPU time limit exceeded.
- **exit(159/153):** It indicates that a program was aborted (received **SIGXFSZ**), perhaps as a result of File size limit exceeded.

<br><br>
### References
<br><br>
C documentation: [https://devdocs.io/c](https://devdocs.io/c)
<br><br>
Geeksforgeeks (2020). Exit codes in C/C++ with Examples. [online] GeeksforGeeks. Available at: [https://www.geeksforgeeks.org/exit-codes-in-c-c-with-examples/](https://www.geeksforgeeks.org/exit-codes-in-c-c-with-examples/) [Accessed 14 Dec. 2022].
‌<br><br>
Geeksforgeeks (2017). Escape Sequences in C. [online] GeeksforGeeks. Available at: [https://www.geeksforgeeks.org/escape-sequences-c/](https://www.geeksforgeeks.org/escape-sequences-c/) [Accessed 14 Dec. 2022].
‌