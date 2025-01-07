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
