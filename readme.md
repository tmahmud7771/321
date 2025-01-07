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
