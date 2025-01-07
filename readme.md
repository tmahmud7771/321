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

# Linux System Calls and Process Management Guide

## Table of Contents

1. [System Call Basics](#system-call-basics)
2. [File Operations](#file-operations)
3. [Process Management](#process-management)
4. [Lab Tasks Solutions](#lab-tasks-solutions)

## System Call Basics

A system call is an interface between a user program and the Linux kernel. Key system calls covered:

```c
open()  - Open/create files
read()  - Read from files
write() - Write to files
close() - Close file descriptors
wait()  - Wait for child process
fork()  - Create new process
exec()  - Execute a program
```

### Common File Operations

#### 1. Opening Files (open)

```c
int open(const char *pathname, int flags, mode_t mode);

// Common flags:
O_RDONLY  - Read only
O_WRONLY  - Write only
O_RDWR    - Read and write
O_CREAT   - Create if doesn't exist
O_APPEND  - Append mode
O_TRUNC   - Truncate if exists
```

#### 2. Reading and Writing (read/write)

```c
ssize_t read(int fd, void *buf, size_t count);
ssize_t write(int fd, const void *buf, size_t count);

// Example:
char buffer[100];
read(fd, buffer, sizeof(buffer));  // Read up to 100 bytes
write(fd, "Hello", 5);            // Write 5 bytes
```

#### 3. File Position (lseek)

```c
off_t lseek(int fd, off_t offset, int whence);

// whence options:
SEEK_SET - Start of file
SEEK_CUR - Current position
SEEK_END - End of file

// Examples:
lseek(fd, 0, SEEK_SET);    // Go to beginning
lseek(fd, -5, SEEK_END);   // 5 bytes from end
lseek(fd, 10, SEEK_CUR);   // 10 bytes forward
```

## Process Management

### Fork System Call

Creates a new process by duplicating the calling process:

```c
pid_t fork(void);

// Return values:
// < 0  - Error
// = 0  - In child process
// > 0  - In parent process (value is child's PID)

pid_t pid = fork();
if (pid < 0) {
    // Error handling
} else if (pid == 0) {
    // Child process code
} else {
    // Parent process code
}
```

### Wait System Call

Waits for child process to terminate:

```c
pid_t wait(int *status);
pid_t waitpid(pid_t pid, int *status, int options);

// Example:
int status;
wait(&status);  // Wait for any child
waitpid(pid, &status, 0);  // Wait for specific child
```

### Exec Family

Replaces current process with a new program:

```c
execl(path, arg0, arg1, ..., NULL);
execv(path, args[]);
execve(path, args[], env[]);

// Example:
execl("/bin/ls", "ls", "-l", NULL);
```

## Lab Tasks Solutions

### Task 1: Process Creation Depth Analysis

```c
#include <sys/types.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>

#define FORK_DEPTH 3

int main() {
    int i, r;
    pid_t my_pid;
    my_pid = getpid();

    for (i = 1; i <= FORK_DEPTH; i++) {
        r = fork();
        if (r > 0) {
            printf("Parent process %d forked child process %d\n", my_pid, r);
        } else if (r == 0) {
            my_pid = getpid();
            if (i == FORK_DEPTH) {
                r = execl("/bin/echo", "/bin/echo", "Hello World", NULL);
                exit(1);
            }
        } else {
            exit(1);
        }
    }
    return 0;
}
```

Questions and Answers:

1. Value of `i` in parent and child after fork:

   - Parent: Keeps its value of i in the loop
   - Child: Inherits same value of i from parent when fork happens
   - Each process continues with its own copy

2. Value of `my_pid` in parent after child updates:

   - Parent's my_pid stays unchanged
   - Child gets new pid via getpid()
   - Memory is separate after fork

3. Process ID of /bin/echo:

   - Gets new PID assigned by system
   - Original process is replaced by execl()
   - Can be seen using ps command while running

4. Why code after execl not reached:

   - execl completely replaces process image
   - Only fails if error occurs
   - Process memory is overwritten

5. Number of "Hello World" prints:

   - FORK_DEPTH = 3 means 2³ = 8 processes
   - Only leaf processes print
   - Total prints = 4 times

6. Total processes created:
   - Initial process = 1
   - Level 1: 2 processes
   - Level 2: 4 processes
   - Level 3: 8 processes total
   - Formula: 2^FORK_DEPTH = 8

### Task 2: File Writing Program

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char teststr[] = "The quick brown fox jumps over the lazy dog.\n";

int main() {
    int fd;
    int len;
    ssize_t r;

    // Open file with write only and create if not exists
    fd = open("testfile", O_WRONLY | O_CREAT, 0600);
    if (fd < 0) {
        perror("File open failed");
        exit(1);
    }

    len = strlen(teststr);
    printf("Attempting to write %d bytes\n", len);

    r = write(fd, teststr, len);
    if (r < 0) {
        perror("File write failed");
        exit(1);
    }

    printf("Wrote %d bytes\n", (int)r);
    close(fd);
    return 0;
}
```

Questions and Answers:

1. Program functionality:

   - Opens/creates file named "testfile"
   - Writes test string to file
   - Reports number of bytes written
   - Output will show:
     ```
     Attempting to write 44 bytes
     Wrote 44 bytes
     ```

2. Alternative file open modes:

   - O_RDONLY: Read only access
   - O_RDWR: Read and write access

3. open() return value (fd):
   - Success: Returns positive integer (file descriptor)
   - Failure: Returns -1
   - fd used for subsequent read/write operations

### Task 3: File Position and Multiple Writes

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char teststr[] = "The quick brown fox jumps over the lazy dog.\n";

int main() {
    int fd;
    int len;
    ssize_t r;
    off_t off;

    fd = open("testfile2", O_WRONLY | O_CREAT, 0600);
    if (fd < 0) {
        perror("File open failed");
        exit(1);
    }

    len = strlen(teststr);
    printf("Attempting to write %d bytes\n", len);

    // First write
    r = write(fd, teststr, len);
    if (r < 0) {
        perror("File write failed");
        exit(1);
    }
    printf("Wrote %d bytes\n", (int)r);

    // Seek to position 5
    off = lseek(fd, 5, SEEK_SET);
    if (off < 0) {
        perror("File lseek failed");
        exit(1);
    }

    // Second write
    r = write(fd, teststr, len);
    if (r < 0) {
        perror("File write failed");
        exit(1);
    }
    printf("Wrote %d bytes\n", (int)r);

    close(fd);
    return 0;
}
```

Questions and Answers:

1. File size after writes:

   - First write: 44 bytes
   - Seek to position 5
   - Second write: 44 bytes starting at position 5
   - Total size: 44 bytes (overlapping content)

2. lseek effect:

   - Moves file pointer to absolute position 5
   - Second write overwrites from position 5
   - Changes file content but not size

3. Additional seek options:
   - SEEK_CUR: Relative to current position
   - SEEK_END: Relative to end of file
   - Both support positive/negative offsets

### Task 4: Directory Operations

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <errno.h>

int main() {
    int r;

    // Change to parent directory
    r = chdir("..");
    if (r < 0) {
        perror("Eek!");
        exit(1);
    }

    // Execute ls command
    r = execl("/bin/ls", "/bin/ls", NULL);
    perror("Double eek!");  // Only reached if execl fails
    return 0;
}
```

Questions and Answers:

1. Code functionality:

   - Changes current working directory to parent (..)
   - Executes ls command in that directory
   - Shows directory contents
   - Error handling for both operations

2. Shell directory unchanged:

   - chdir only affects current process
   - Shell is parent process
   - Directory changes don't propagate to parent
   - Each process has own working directory

3. /bin/ls directory context:
   - Runs in parent directory (..)
   - Because chdir executed before execl
   - New process inherits working directory
   - Would need to change back if needed

### Task 1: Process Creation and Fork Depth

Analysis of the code:

```c
#define FORK_DEPTH 3

// Questions and Answers:
// 1. Value of i in parent and child after fork:
//    Parent: retains current value of i
//    Child: inherits same value of i as parent

// 2. Value of my_pid in parent after child updates:
//    Parent's my_pid remains unchanged because child's
//    update only affects child's copy

// 3. Process ID of /bin/echo:
//    New PID assigned by system when execl runs

// 4. Why code after execl not reached:
//    execl replaces entire process image, so following
//    code never executes unless execl fails

// 5. Hello World printed when FORK_DEPTH is 3:
//    Printed once per leaf process = 4 times

// 6. Total processes created (including first):
//    2^FORK_DEPTH = 2^3 = 8 processes
```

### Task 2: File Operations

Analysis of file writing program:

```c
// Questions and Answers:

// 1. Code functionality:
//    - Opens/creates file "testfile"
//    - Writes test string to file
//    - Reports bytes written
//    Output will be:
//    Attempting to write 44 bytes
//    Wrote 44 bytes

// 2. Other ways to open file besides O_WRONLY:
//    - O_RDONLY (read only)
//    - O_RDWR (read and write)

// 3. open() return value (fd):
//    Success: Returns non-negative integer (file descriptor)
//    Failure: Returns -1
//    fd is used as handle for all subsequent operations
```

### Task 3: File Position and Multiple Writes

Analysis of lseek and multiple writes:

```c
// Questions and Answers:

// 1. File size after two writes:
//    44 + 44 = 88 bytes (full string written twice)

// 2. lseek effect:
//    Moves file pointer to position 5,
//    Second write starts from that position

// 3. Additional seek options:
//    - SEEK_CUR (current position)
//    - SEEK_END (end of file)
```

### Task 4: Directory Operations

Analysis of directory change and exec:

```c
// Questions and Answers:

// 1. Code functionality:
//    - Changes to parent directory (..)
//    - Executes ls command
//    - Shows error if either operation fails

// 2. Shell working directory unchanged because:
//    chdir only affects the current process
//    Parent shell is separate process

// 3. /bin/ls directory:
//    Runs in the parent directory (..)
//    Because chdir changed directory before exec
```

## Common Pitfalls and Tips

1. **File Descriptors:**

   - Always check return values
   - Close files when done
   - Don't assume operations succeed

2. **Process Management:**

   - Fork creates exact copy
   - Child/parent run concurrently
   - exec replaces current process
   - Wait prevents zombie processes

3. **Error Handling:**

   ```c
   if (fd < 0) {
       perror("Error message");
       exit(1);
   }
   ```

4. **Memory and Resources:**
   - File descriptors are inherited by child processes
   - Memory is copied in fork (copy-on-write)
   - exec releases old process resources

## Common Use Cases

1. **File Copy Program:**

```c
int source_fd = open("source.txt", O_RDONLY);
int dest_fd = open("dest.txt", O_WRONLY | O_CREAT, 0644);
char buffer[1024];
ssize_t bytes;

while ((bytes = read(source_fd, buffer, sizeof(buffer))) > 0) {
    write(dest_fd, buffer, bytes);
}
```

2. **Process Creation with Pipe:**

```c
int pipefd[2];
pipe(pipefd);
pid_t pid = fork();

if (pid == 0) {
    // Child reads
    close(pipefd[1]);
    read(pipefd[0], buffer, sizeof(buffer));
} else {
    // Parent writes
    close(pipefd[0]);
    write(pipefd[1], "message", 7);
}
```

3. **Command Execution:**

```c
if (fork() == 0) {
    execl("/bin/command", "command", "arg1", "arg2", NULL);
    exit(1);  // Only reaches here if exec fails
}
wait(NULL);  // Parent waits for child
```

# POSIX Threads (pthreads) Cheat Sheet

## Table of Contents

- [Basic Concepts](#basic-concepts)
- [Common Functions](#common-functions)
- [Compilation](#compilation)
- [Example Tasks](#example-tasks)
- [Common Patterns](#common-patterns)
- [Best Practices](#best-practices)

## Basic Concepts

POSIX Threads (pthreads) is a standardized API for creating and managing threads in C programming. It's particularly useful for:

- Parallel processing
- Concurrent execution
- Multi-core utilization
- Background tasks

### Required Header

```c
#include <pthread.h>
```

## Common Functions

### Thread Creation

```c
int pthread_create(pthread_t *thread_id,
                  const pthread_attr_t *attr,
                  void *(*thread_function)(void *),
                  void *arg);
```

- `thread_id`: Pointer to store the thread ID
- `attr`: Thread attributes (NULL for defaults)
- `thread_function`: Function to be executed by thread
- `arg`: Arguments to pass to the thread function

### Thread Termination

```c
void pthread_exit(void *return_value);
```

- Terminates the calling thread
- `return_value`: Value to be returned to pthread_join()

### Thread Joining

```c
int pthread_join(pthread_t thread_id, void **thread_return);
```

- Waits for specified thread to terminate
- `thread_return`: Pointer to store the thread's return value

## Compilation

To compile programs using pthreads:

```bash
gcc -o program_name source_file.c -lpthread
```

## Example Tasks

### Task 1: Basic Thread Creation and Parallel Execution

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

void func1(void);
void *funcThread(void *arg);

int main() {
    pthread_t t1;
    pthread_create(&t1, NULL, funcThread, NULL);
    func1();
    pthread_join(t1, NULL);
    return 0;
}

void func1() {
    printf("Entered func1:\n");
    for(int i = 0; i < 5; i++) {
        printf("func1: %d\n", i);
        sleep(1);
    }
    printf("Done with func 1....\n");
}

void *funcThread(void *arg) {
    printf("Entered thread1:\n");
    for(int i = 0; i < 5; i++) {
        printf("thread: %d\n", i);
        sleep(1);
    }
    printf("Done with thread 1....\n");
    return NULL;
}
```

Purpose: Demonstrates basic thread creation and parallel execution of two functions.

### Task 2: Thread Return Values

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

void *func_thread(int *n);
void *t_ret;
int num = 3;

int main() {
    pthread_t t1;
    pthread_create(&t1, NULL, (void *)func_thread, &num);
    pthread_join(t1, &t_ret);
    printf("Thread returned: %s\n", (char *)t_ret);
    return 0;
}

void *func_thread(int *n) {
    printf("Entered in Thread:\n");
    if(*n % 2 == 0) {
        pthread_exit("Even");
    } else {
        pthread_exit("Odd");
    }
}
```

Purpose: Shows how to return values from threads using pthread_exit().

### Task 3: Multiple Threads with Different Functions

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

void *t_func1(void *arg);
void *t_func2(void *arg1);
int t_id[2] = {1, 2};
int a = 10;
int b = 5;

int main() {
    int a1[3] = {t_id[0], a, b};
    int a2[3] = {t_id[1], a, b};
    pthread_t t1, t2;

    pthread_create(&t1, NULL, t_func1, (void *)a1);
    pthread_create(&t2, NULL, t_func2, (void *)a2);

    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    return 0;
}

void *t_func1(void *arg) {
    int *x = arg;
    printf("Entered in Thread :%d\n", x[0]);
    sleep(1);
    int add = x[1] + x[2];
    printf("ADD :%d\n", add);
    printf("Addition Done by Thread %d...\n", x[0]);
    return NULL;
}

void *t_func2(void *arg1) {
    int *y = arg1;
    printf("Entered in Thread :%d\n", y[0]);
    sleep(1);
    int sub = y[1] - y[2];
    printf("SUB :%d\n", sub);
    printf("Subtraction Done by Thread %d...\n", y[0]);
    return NULL;
}
```

Purpose: Demonstrates creating multiple threads with different functions and passing arrays as arguments.

### Task 4: Multiple Threads with Same Function

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

int t_id[2] = {1, 2};
void *t_func(int *id);

int main() {
    pthread_t t[2];
    pthread_create(&t[0], NULL, (void *)t_func, &t_id[0]);
    pthread_create(&t[1], NULL, (void *)t_func, &t_id[1]);

    for(int i = 0; i < 2; i++) {
        pthread_join(t[i], NULL);
    }

    return 0;
}

void *t_func(int *id) {
    printf("Entered in Thread %d...\n", *id);
    for(int i = 0; i < 5; i++) {
        printf("Thread %d Turn %d\n", *id, i);
        sleep(1);
    }
    printf("Ending Thread %d...\n", *id);
    return NULL;
}
```

Purpose: Shows how to create multiple threads using the same function with different arguments.

## Common Patterns

### Passing Multiple Arguments

To pass multiple arguments to a thread function:

1. Create a struct containing all parameters

```c
struct thread_args {
    int arg1;
    char *arg2;
    float arg3;
};
```

2. Pass the struct to pthread_create

```c
struct thread_args args = {1, "hello", 3.14};
pthread_create(&thread, NULL, thread_function, (void *)&args);
```

### Thread Safety

1. Use local variables when possible
2. Protect shared resources with mutex locks
3. Avoid global variables unless necessary
4. Use atomic operations for simple shared variables

## Best Practices

1. Always check return values of pthread functions

```c
if (pthread_create(&thread, NULL, function, arg) != 0) {
    perror("pthread_create failed");
    exit(1);
}
```

2. Always join or detach threads

```c
pthread_join(thread, NULL);  // For joinable threads
// or
pthread_detach(thread);      // For detached threads
```

3. Free resources before thread termination

```c
void *thread_function(void *arg) {
    void *resource = malloc(size);
    // ... use resource ...
    free(resource);
    return NULL;
}
```

4. Initialize mutex and condition variables before use

```c
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;
```

5. Always include proper error handling

```c
if (pthread_mutex_lock(&mutex) != 0) {
    // Handle error
}
```

## Common Issues and Solutions

1. Deadlocks

   - Always acquire locks in the same order
   - Use pthread_mutex_trylock() when appropriate
   - Implement timeout mechanisms

2. Race Conditions

   - Use mutex locks for shared resources
   - Minimize the critical section
   - Use atomic operations when possible

3. Memory Leaks
   - Free dynamically allocated resources
   - Join or detach all created threads
   - Clean up synchronization objects (mutex, condition variables)

Remember: Multithreaded programming requires careful consideration of synchronization, resource sharing, and thread safety. Always test thoroughly for race conditions and deadlocks.

# Lab 7: Semaphores and Mutexes in Linux

> A comprehensive guide to understanding synchronization primitives in POSIX threads

## Table of Contents

- [Key Concepts](#key-concepts)
- [Semaphores](#semaphores)
  - [What are Semaphores?](#what-are-semaphores)
  - [Semaphore Functions](#semaphore-functions)
  - [Example with Semaphores](#example-with-semaphores)
- [Mutexes](#mutexes)
  - [What are Mutexes?](#what-are-mutexes)
  - [Mutex Functions](#mutex-functions)
  - [Example with Mutex](#example-with-mutex)
- [Comparison: Race Condition Example](#comparison-race-condition-example)

## Key Concepts

1. **Synchronization**: Coordinating multiple threads/processes to prevent race conditions
2. **Race Condition**: When multiple threads access shared resources simultaneously
3. **Critical Section**: Code section where shared resources are accessed
4. **Thread Safety**: Ensuring correct program behavior with multiple threads

## Semaphores

### What are Semaphores?

A semaphore is an integer counter used for synchronization with two main operations:

- **wait** (decrement): Reduces count by 1
- **post** (increment): Increases count by 1

Types of Semaphores:

1. **Binary Semaphore**: Values limited to 0 and 1
2. **Counting Semaphore**: Can have arbitrary values

### Semaphore Functions

```c
// Required header
#include <semaphore.h>

// Function prototypes
int sem_init(sem_t *sem, int pshared, unsigned int value);
int sem_wait(sem_t *sem);
int sem_post(sem_t *sem);
int sem_destroy(sem_t *sem);
```

Function Details:

1. **sem_init**:

   - Initializes semaphore
   - Parameters:
     - `sem`: Pointer to semaphore
     - `pshared`: 0 for threads, 1 for processes
     - `value`: Initial value
   - Returns: 0 on success, -1 on failure

2. **sem_wait**:

   - Decrements semaphore
   - Blocks if value is 0
   - Returns: 0 on success, -1 on failure

3. **sem_post**:

   - Increments semaphore
   - Returns: 0 on success, -1 on failure

4. **sem_destroy**:
   - Destroys semaphore
   - Returns: 0 on success, -1 on failure

### Example with Semaphores

```c
// Basic semaphore usage
sem_t s;
sem_init(&s, 0, 1);    // Initialize with value 1
sem_wait(&s);          // Enter critical section
// ... critical section code ...
sem_post(&s);          // Exit critical section
sem_destroy(&s);       // Clean up
```

## Mutexes

### What are Mutexes?

A mutex (mutual exclusion) is a binary semaphore with ownership restriction:

- Can only be unlocked by the thread that locked it
- Used for protecting shared resources
- Simpler than semaphores but less flexible

### Mutex Functions

```c
// Required header
#include <pthread.h>

// Function prototypes
int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutexattr_t *attr);
int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_unlock(pthread_mutex_t *mutex);
int pthread_mutex_destroy(pthread_mutex_t *mutex);
```

Function Details:

1. **pthread_mutex_init**:

   - Initializes mutex
   - Parameters:
     - `mutex`: Pointer to mutex
     - `attr`: Mutex attributes (NULL for defaults)
   - Returns: 0 on success, error code on failure

2. **pthread_mutex_lock**:

   - Locks mutex
   - Blocks if already locked
   - Returns: 0 on success, error code on failure

3. **pthread_mutex_unlock**:

   - Unlocks mutex
   - Must be called by same thread that locked it
   - Returns: 0 on success, error code on failure

4. **pthread_mutex_destroy**:
   - Destroys mutex
   - Returns: 0 on success, error code on failure

### Example with Mutex

```c
// Basic mutex usage
pthread_mutex_t mutex;
pthread_mutex_init(&mutex, NULL);     // Initialize mutex
pthread_mutex_lock(&mutex);           // Enter critical section
// ... critical section code ...
pthread_mutex_unlock(&mutex);         // Exit critical section
pthread_mutex_destroy(&mutex);        // Clean up
```

## Comparison: Race Condition Example

Here's a comparison showing how race conditions occur and how to fix them:

1. **Without Protection (Race Condition)**:

```c
// From cs.c
void *t_func(int *id) {
    for(int i=0; i<100000; i++) {
        count++;  // Race condition here!
    }
}
```

2. **With Mutex Protection**:

```c
// From Mutex.c
void *t_func(int *id) {
    for(int i=0; i<100000; i++) {
        pthread_mutex_lock(&mutex);
        count++;  // Protected from race condition
        pthread_mutex_unlock(&mutex);
    }
}
```

3. **With Semaphore Protection**:

```c
// From sem1.c
void *t_func(int *id) {
    for(int i=0; i<100000; i++) {
        sem_wait(&s);
        count++;  // Protected from race condition
        sem_post(&s);
    }
}
```

## Common Mistakes to Avoid

1. **Deadlocks**:

   - Not releasing locks in correct order
   - Holding multiple locks simultaneously

2. **Race Conditions**:

   - Forgetting to protect shared resources
   - Insufficient synchronization

3. **Resource Leaks**:
   - Not destroying mutexes/semaphores
   - Not properly initializing synchronization primitives

## Compilation

Always compile with pthread library:

```bash
gcc -pthread your_program.c -o your_program
```

## Key Differences: Mutex vs Semaphore

1. **Ownership**:

   - Mutex: Has owner (thread that locked it)
   - Semaphore: No ownership concept

2. **Usage**:

   - Mutex: Binary (locked/unlocked)
   - Semaphore: Can count resources

3. **Purpose**:
   - Mutex: Exclusive access to shared resource
   - Semaphore: Synchronization and resource management

This cheatsheet covers the essential concepts and usage patterns for POSIX threads synchronization primitives. Use it as a quick reference when working with concurrent programming in C.

## Example Programs Analysis

### 1. Basic Threading (cs.c)

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

int t_id[2]={1,2};
void *t_func(int *id);
int count=0;

int main() {
    pthread_t t[2];
    pthread_create(&t[0], NULL, (void *)t_func, &t_id[0]);
    pthread_create(&t[1], NULL, (void *)t_func, &t_id[1]);

    for(int i=0; i<2; i++) {
        pthread_join(t[i], NULL);
    }

    printf("Total count: %d\n", count);
    return 0;
}

void *t_func(int *id) {
    printf("Entered in Thread %d...\n", *id);
    for(int i=0; i<100000; i++) {
        count++;  // Race condition here!
    }
}
```

**Analysis of cs.c**:

- Creates 2 threads that increment a shared counter
- Has a race condition because multiple threads access `count` without synchronization
- Final count will be unpredictable and less than expected 200,000
- Demonstrates why synchronization is needed

### 2. Using Mutex (Mutex.c)

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

int t_id[2]={1,2};
void *t_func(int *id);
int count=0;
pthread_mutex_t mutex;

int main() {
    pthread_t t[2];
    pthread_mutex_init(&mutex, NULL);
    pthread_create(&t[0], NULL, (void *)t_func, &t_id[0]);
    pthread_create(&t[1], NULL, (void *)t_func, &t_id[1]);

    for(int i=0; i<2; i++) {
        pthread_join(t[i], NULL);
    }

    pthread_mutex_destroy(&mutex);
    printf("Total count: %d\n", count);
    return 0;
}

void *t_func(int *id) {
    printf("Entered in Thread %d...\n", *id);
    for(int i=0; i<100000; i++) {
        pthread_mutex_lock(&mutex);
        count++;
        pthread_mutex_unlock(&mutex);
    }
}
```

**Analysis of Mutex.c**:

- Fixes race condition using mutex
- Only one thread can increment count at a time
- Final count will always be 200,000
- Shows proper mutex initialization, locking, and cleanup

### 3. Using Binary Semaphore (sem1.c)

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>
#include <semaphore.h>

int t_id[4]={1,2,3,4};
void *t_func(int *id);
int count=0;
sem_t s;

int main() {
    pthread_t t[4];
    sem_init(&s, 0, 1);

    for(int i=0; i<4; i++) {
        pthread_create(&t[i], NULL, (void *)t_func, &t_id[i]);
    }

    for(int i=0; i<4; i++) {
        pthread_join(t[i], NULL);
    }

    sem_destroy(&s);
    printf("Total count: %d\n", count);
    return 0;
}

void *t_func(int *id) {
    printf("Entered in Thread %d...\n", *id);
    for(int i=0; i<100000; i++) {
        sem_wait(&s);
        count++;
        sem_post(&s);
    }
}
```

**Analysis of sem1.c**:

- Uses binary semaphore (initialized to 1)
- Similar to mutex but works with 4 threads
- Protects critical section using sem_wait/sem_post
- Final count will be 400,000 (4 threads \* 100,000)

### 4. Semaphore for Thread Ordering (sem2.c)

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>
#include <semaphore.h>

int t_id[4]={1,2,3,4};
void *t_func(int *id);
sem_t s;

int main() {
    pthread_t t[4];
    sem_init(&s, 0, 1);

    for(int i=0; i<4; i++) {
        pthread_create(&t[i], NULL, (void *)t_func, &t_id[i]);
    }

    for(int i=0; i<4; i++) {
        pthread_join(t[i], NULL);
    }

    sem_destroy(&s);
    return 0;
}

void *t_func(int *id) {
    sem_wait(&s);
    sleep(1);
    printf("Entered in Thread %d...\n", *id);
    sem_post(&s);
}
```

**Analysis of sem2.c**:

- Demonstrates thread ordering using semaphore
- Each thread must wait its turn to print
- sleep(1) makes the ordering more visible
- Shows how semaphores can control access to any resource, not just counters

### Key Differences in the Examples:

1. **Thread Count**:

   - cs.c and Mutex.c: 2 threads
   - sem1.c and sem2.c: 4 threads

2. **Synchronization Method**:

   - cs.c: None (shows race condition)
   - Mutex.c: Mutex (ownership-based)
   - sem1.c: Semaphore for counting
   - sem2.c: Semaphore for ordering

3. **Purpose**:
   - cs.c: Shows problem
   - Mutex.c: Shows basic solution
   - sem1.c: Shows scaling to more threads
   - sem2.c: Shows thread ordering

### Program Output Examples:

1. **cs.c** (incorrect due to race condition):

```
Entered in Thread 1...
Entered in Thread 2...
Total count: 143762  // Number will vary each run
```

2. **Mutex.c** (correct with synchronization):

```
Entered in Thread 1...
Entered in Thread 2...
Total count: 200000  // Always correct
```

3. **sem1.c** (correct with 4 threads):

```
Entered in Thread 1...
Entered in Thread 2...
Entered in Thread 3...
Entered in Thread 4...
Total count: 400000  // Always correct
```

4. **sem2.c** (ordered execution):

```
Entered in Thread 1...
Entered in Thread 2...
Entered in Thread 3...
Entered in Thread 4...  // One at a time, with 1-second gaps
```
