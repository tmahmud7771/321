# Linux Shell Commands Cheatsheet

## System Information

- `uname` - Display system information
- `whoami` - Show current user name
- `man [command]` - Display manual for specified command

## File Creation & Editing

- `touch [file]` - Create empty file(s)
- `cat > [file]` - Create file and write content (Ctrl+D to save)
- `cat [file]` - Display file content
- `cat [file1] [file2] > [file3]` - Concatenate files

## File Operations

- `cp [src] [dest]` - Copy files/directories

  - `-i` - Prompt before overwrite
  - `-r` - Copy directories recursively
  - `-u` - Copy only when source is newer

- `rm [file]` - Remove files/directories

  - `-f` - Force remove without prompt
  - `-i` - Prompt before removal
  - `-r` - Remove directories recursively
  - `-v` - Verbose output

- `mv [src] [dest]` - Move/rename files
  - `-i` - Prompt before overwrite
  - `-u` - Move only when source is newer
  - `-v` - Verbose output

## Directory Operations

- `ls` - List directory contents
  - `-a` - Show hidden files
  - `-A` - Show hidden files except . and ..
  - `-h` - Human readable sizes
  - `-l` - Long format listing
  - `-S` - Sort by file size

## File Permissions

- `chmod [permissions] [file]` - Change file permissions
  - Format: `[who][+/-/=][permissions]`
  - who: u (user), g (group), o (others), a (all)
  - permissions: r (read), w (write), x (execute)
  - Example: `chmod go+rw file1` - Add read/write for group/others

## Input/Output Redirection

- `<` - Input redirection from file
- `>` - Output redirection to file (overwrite)
- `>>` - Output redirection to file (append)

## Calculator (bc)

- `bc` - Start calculator
- `scale=[n]` - Set decimal precision
- `ibase=[n]` - Set input base
- `obase=[n]` - Set output base
- `quit` - Exit calculator

## Additional Tools

- `factor [n]` - Display prime factors of a number
- `cal` - Display calendar
  - `cal [year]` - Show calendar for specific year
  - `cal [month] [year]` - Show calendar for specific month/year

## File Types

- `-` - Regular file
- `d` - Directory
- `c` - Character special file
- `b` - Block special file
- `l` - Symbolic link
- `s` - Socket
- `p` - Named pipe
- `m` - Shared memory file

# C Programming Fundamentals and Lab Solutions

## Table of Contents

1. [Basic Program Structure](#basic-program-structure)
2. [Data Types](#data-types)
3. [Input/Output](#inputoutput)
4. [Arrays](#arrays)
5. [Pointers](#pointers)
6. [Strings](#strings)
7. [Structures](#structures)
8. [Lab Solutions](#lab-solutions)

## Basic Program Structure

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    printf("Hello World!\n");
    return EXIT_SUCCESS;
}
```

- Every C program starts execution from main()
- Include required header files using #include
- Return EXIT_SUCCESS (0) to indicate successful execution

## Data Types

Common data types in C:

```c
int main() {
    char character = 'A';         // Single character
    int number = 42;             // Integer
    float decimal = 3.14f;       // Single-precision floating point
    double precise = 3.141592;   // Double-precision floating point
    void *pointer = NULL;        // Void pointer

    printf("Size of int: %lu bytes\n", sizeof(int));
    return 0;
}
```

## Input/Output

### Basic Input

```c
int number;
char str[100];

// Reading integer
scanf("%d", &number);

// Reading string
scanf("%s", str);

// Reading character
char ch = getchar();
```

### Basic Output

```c
int num = 42;
printf("Number is: %d\n", num);
printf("Float with 2 decimals: %.2f\n", 3.14159);
```

## Arrays

### One-dimensional Array

```c
int numbers[5] = {1, 2, 3, 4, 5};

// Accessing elements
for(int i = 0; i < 5; i++) {
    printf("%d ", numbers[i]);
}
```

### Multi-dimensional Array

```c
int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};

// Accessing elements
for(int i = 0; i < 2; i++) {
    for(int j = 0; j < 3; j++) {
        printf("%d ", matrix[i][j]);
    }
    printf("\n");
}
```

## Pointers

```c
int var = 20;
int *ptr = &var;    // Store address of var in pointer

printf("Value of var: %d\n", var);
printf("Address of var: %p\n", (void*)&var);
printf("Value at pointer: %d\n", *ptr);
```

### Pointer Arithmetic

```c
int arr[] = {10, 20, 30, 40, 50};
int *ptr = arr;

// Increment pointer
ptr++;  // Points to next element
```

## Strings

```c
// String declaration
char str1[] = "Hello";
char str2[20];

// String functions (include <string.h>)
strlen(str1);      // Length of string
strcpy(str2, str1); // Copy str1 to str2
strcat(str2, str1); // Concatenate str1 to str2
strcmp(str1, str2); // Compare strings
```

## Structures

```c
struct Student {
    char name[50];
    int roll_number;
    float marks;
};

// Using structure
struct Student s1 = {"John", 1, 85.5};
printf("Name: %s\n", s1.name);
```

## Lab Solutions

### 1. Print Personal Information

```c
#include <stdio.h>

int main() {
    printf("Name: John Doe\n");
    printf("Date of Birth: 01/01/2000\n");
    printf("Mobile: +1-234-567-8900\n");
    return 0;
}
```

### 2. Rectangle Area and Perimeter

```c
#include <stdio.h>

int main() {
    int height = 7, width = 5;
    int perimeter = 2 * (height + width);
    int area = height * width;

    printf("Perimeter: %d inches\n", perimeter);
    printf("Area: %d square inches\n", area);
    return 0;
}
```

### 3. Circle Area and Perimeter

```c
#include <stdio.h>
#define PI 3.14159

int main() {
    float radius;
    printf("Enter radius: ");
    scanf("%f", &radius);

    float perimeter = 2 * PI * radius;
    float area = PI * radius * radius;

    printf("Perimeter: %.2f\n", perimeter);
    printf("Area: %.2f\n", area);
    return 0;
}
```

### 4. Store and Print Array

```c
#include <stdio.h>

int main() {
    int arr[5];
    printf("Enter 5 numbers:\n");

    for(int i = 0; i < 5; i++) {
        scanf("%d", &arr[i]);
    }

    printf("Array elements: ");
    for(int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

### 5. Reverse Array

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter size of array: ");
    scanf("%d", &n);

    int arr[n];
    printf("Enter %d numbers:\n", n);
    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    printf("Reversed array: ");
    for(int i = n-1; i >= 0; i--) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

### 6. Seconds to Hours, Minutes, Seconds

```c
#include <stdio.h>

int main() {
    int totalSeconds, hours, minutes, seconds;

    printf("Enter seconds: ");
    scanf("%d", &totalSeconds);

    hours = totalSeconds / 3600;
    minutes = (totalSeconds % 3600) / 60;
    seconds = totalSeconds % 60;

    printf("%d:%d:%d\n", hours, minutes, seconds);
    return 0;
}
```

### 7. Swap Variables

```c
#include <stdio.h>

int main() {
    int a, b, temp;

    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);

    temp = a;
    a = b;
    b = temp;

    printf("After swap: %d %d\n", a, b);
    return 0;
}
```

### 8. ASCII Value

```c
#include <stdio.h>

int main() {
    char ch;
    printf("Enter a character: ");
    scanf("%c", &ch);
    printf("ASCII value of %c is %d\n", ch, ch);
    return 0;
}
```

### 9. Concatenate Strings

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str1[50], str2[50];

    printf("Enter first string: ");
    scanf("%s", str1);
    printf("Enter second string: ");
    scanf("%s", str2);

    strcat(str1, str2);
    printf("Concatenated string: %s\n", str1);
    return 0;
}
```

### 10. Student Information using Struct

```c
#include <stdio.h>
#include <string.h>

struct Student {
    char name[50];
    int roll_number;
    float marks;
};

int main() {
    struct Student s1;

    printf("Enter name: ");
    scanf("%s", s1.name);
    printf("Enter roll number: ");
    scanf("%d", &s1.roll_number);
    printf("Enter marks: ");
    scanf("%f", &s1.marks);

    printf("\nStudent Information:\n");
    printf("Name: %s\n", s1.name);
    printf("Roll Number: %d\n", s1.roll_number);
    printf("Marks: %.2f\n", s1.marks);

    return 0;
}
```

# Advanced C Programming Concepts and Solutions

## Table of Contents

1. [Control Flow Statements](#control-flow)
2. [Loops](#loops)
3. [Functions](#functions)
4. [File I/O](#file-io)
5. [Command Line Arguments](#command-line)
6. [Lab Solutions](#lab-solutions)

## Control Flow

### If Statement

```c
if (condition) {
    // code block
} else if (another_condition) {
    // code block
} else {
    // code block
}

// Example:
int a = 100;
if (a < 20) {
    printf("a is less than 20\n");
} else {
    printf("a is not less than 20\n");
}
```

## Loops

### While Loop

```c
// Basic while loop
int a = 10;
while (a < 20) {
    printf("value of a: %d\n", a);
    a++;
}
```

### For Loop

```c
// Basic for loop
for(int a = 10; a < 20; a++) {
    printf("value of a: %d\n", a);
}
```

### Nested Loop Example

```c
// Example: Finding prime numbers
for(i=2; i<100; i++) {
    for(j=2; j <= (i/j); j++) {
        if(!(i%j)) break; // if factor found, not prime
    }
    if(j > (i/j)) printf("%d is prime\n", i);
}
```

## Functions

### Function Definition

```c
// Function declaration
return_type function_name(parameters);

// Example function
int max(int num1, int num2) {
    if (num1 > num2)
        return num1;
    else
        return num2;
}
```

### Call by Value vs Call by Reference

#### Call by Value

```c
void swap(int x, int y) {
    int temp;
    temp = x;  // value is copied
    x = y;
    y = temp;
}
```

#### Call by Reference

```c
void swap(int *x, int *y) {
    int temp;
    temp = *x;  // value at address is changed
    *x = *y;
    *y = temp;
}
```

## File I/O

### Basic File Operations

```c
// Opening a file
FILE *fp;
fp = fopen("test.txt", "w+");  // w+ for read and write

// Writing to file
fprintf(fp, "This is test content\n");
fputs("More content\n", fp);

// Reading from file
char buffer[100];
fscanf(fp, "%s", buffer);
fgets(buffer, 255, (FILE*)fp);

// Closing file
fclose(fp);
```

### File Access Modes

- `"r"` - Read only
- `"w"` - Write (file truncated if exists)
- `"a"` - Append
- `"r+"` - Read and write from beginning
- `"w+"` - Read and write (truncated if exists)
- `"a+"` - Read and append (writing at end)

## Command Line Arguments

```c
int main(int argc, char *argv[]) {
    // argc - number of arguments
    // argv[] - array of arguments
    // argv[0] - program name
    // argv[1] - first argument

    if(argc == 2) {
        printf("The argument supplied is %s\n", argv[1]);
    }
    return 0;
}
```

## Lab Solutions

### 1. Vowel or Consonant Checker

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char ch;
    printf("Enter a character: ");
    scanf("%c", &ch);

    ch = tolower(ch);
    if(ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u')
        printf("%c is a vowel\n", ch);
    else
        printf("%c is a consonant\n", ch);

    return 0;
}
```

### 2. Triangle Angle Validator

```c
#include <stdio.h>

int main() {
    int angle1, angle2, angle3;
    printf("Enter three angles: ");
    scanf("%d %d %d", &angle1, &angle2, &angle3);

    if(angle1 + angle2 + angle3 == 180 && angle1 > 0 && angle2 > 0 && angle3 > 0)
        printf("Triangle is valid\n");
    else
        printf("Triangle is not valid\n");

    return 0;
}
```

### 3. Sum of Even Numbers

```c
#include <stdio.h>

int main() {
    int n, sum = 0;
    printf("Enter the value of n: ");
    scanf("%d", &n);

    for(int i = 2; i <= n; i += 2) {
        sum += i;
    }

    printf("Sum of even numbers from 1 to %d is %d\n", n, sum);
    return 0;
}
```

### 4. Array Reversal

```c
#include <stdio.h>

int main() {
    int arr[100], n;
    printf("Enter number of elements: ");
    scanf("%d", &n);

    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    // Reversing array
    for(int i = 0; i < n/2; i++) {
        int temp = arr[i];
        arr[i] = arr[n-1-i];
        arr[n-1-i] = temp;
    }

    printf("Reversed array: ");
    for(int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

### 5. Circle Calculations

```c
#include <stdio.h>
#define PI 3.14159

double getDiameter(double radius) {
    return 2 * radius;
}

double getCircumference(double radius) {
    return 2 * PI * radius;
}

double getArea(double radius) {
    return PI * radius * radius;
}

int main() {
    double radius;
    printf("Enter radius: ");
    scanf("%lf", &radius);

    printf("Diameter: %.2f\n", getDiameter(radius));
    printf("Circumference: %.2f\n", getCircumference(radius));
    printf("Area: %.2f\n", getArea(radius));

    return 0;
}
```

### 6. Array Swap Using References

```c
#include <stdio.h>

void swap(int *x, int *y) {
    int temp = *x;
    *x = *y;
    *y = temp;
}

int main() {
    int arr[100], n;
    printf("Enter array size: ");
    scanf("%d", &n);

    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    for(int i = 0; i < n-1; i += 2) {
        swap(&arr[i], &arr[i+1]);
    }

    printf("After swapping: ");
    for(int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

### 7. File Character Filter

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    FILE *fp;
    char ch;

    fp = fopen("input.txt", "r");
    if(fp == NULL) {
        printf("Error opening file\n");
        return 1;
    }

    while((ch = fgetc(fp)) != EOF) {
        if(isalpha(ch)) {
            printf("%c", ch);
        }
    }

    fclose(fp);
    return 0;
}
```

### 8. Command Line Sorting

```c
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

int main(int argc, char *argv[]) {
    if(argc < 2) {
        printf("Usage: %s number1 number2 ...\n", argv[0]);
        return 1;
    }

    int numbers[100];
    int count = argc - 1;

    for(int i = 0; i < count; i++) {
        numbers[i] = atoi(argv[i + 1]);
    }

    qsort(numbers, count, sizeof(int), compare);

    printf("Sorted numbers: ");
    for(int i = 0; i < count; i++) {
        printf("%d ", numbers[i]);
    }
    printf("\n");

    return 0;
}
```
