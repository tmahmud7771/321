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
