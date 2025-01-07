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
