A **semaphore** is a synchronization primitive type (in `semaphore.h` header) used in to manage access to shared resource
- It helps ensure proper coordination between threads
- preventing race conditions 
- maintaining mutual exclusion

Acts like an integer variable storing value on whether a resource is being utilized. Semaphore value can be changed only with 2 atomic operations: P and V
> [!info]+ Atomic Operation
> An operation that runs without interruption

Types:
- **Binary Semaphore**: Stores whether a resource is being used (0) or if it is free (1). Acts like a mutex lock.
	- if `semaphore = 0` -> process busy-waits until `semaphore = 1`
	- if `semaphore = 1` -> process enters critical section and `semaphore = 0`
- **Counting Semaphore**: Stores the total number of free resources. Enables synchronization over a resource pool.
	- if `semaphore = 0` -> process busy-waits until `semaphore > 0` 
		- Usually, waiting is implemented with waiting queue to prevent busy-waiting taking up processor time.
		- While a process is busy-waiting, the scheduler cannot send other processes which decreases CPU utilization and response times. Hence wait-queue is implemented with counting semaphores.
		- if `semaphore <= 0` -> processes enter waiting queue until `semaphore > 0`. The negative value indicates the amount of processes waiting in queue. when `semaphore > 0` the scheduler sends processes from wait queue (usually FIFO)
	- if `semaphore >= 1` -> process enters critical section and `semaphore = semaphore -1`
		- The value of the semaphore indicates the number of free resources in the pool.

## 1. Semaphore Usage
A semaphore is an integer data-type that can only be changed by atomic operations. It is defined in the `semaphore.h` header file using the `sem_t` data type.
```c
#include <semaphore.h>

sem_t semaphore ;
```
In *glibc*,  a semaphore is implemented as a union data type
```c
typedef union
{
	char __size[__SIZEOF_SEM_T];
	long int __align;
} sem_t;
```

1. **Wait operation**
Syntax: `sem_wait(sem_t *S)`
Definition:
```c
sem_wait(sem_t *S)
{
	while(S <= 0)
		/*busy wait until resource is freed and S == 1*/ ;
	//utilize the freed resource to run the thread. Decrement S to indicate resource utillization
	S--;
}
```
- Wait makes the process/thread busy wait until a resource is freed
- Instead of busy-waiting, a process can be blocked and added to waiting queue
>[!info] What is busy waiting?
-> A **busy waiting** thread **actively checks** for a condition and continually consumes CPU cycles even though it is not able to proceed yet (like checking if semaphore value is +ve yet).
-> The thread does not get blocked or put to sleep. Instead, it keeps looping and checking the condition in a tight loop (polling), wasting CPU resources.

> [!info] What is blocked/suspended?
-> [[Process Blocking]] is a where a process is made to wait for an i/o operation or event to occur (in this case, semaphore calling the process) 
->A **blocked** thread or process **is not using CPU time**. It is put to sleep and will only be resumed once the condition it is waiting for (like a semaphore increment) is met.
-> Typically an I/O operation or the availability of a resource (like a lock) causes thread blocking
-> **No active computation** is taking place while the thread is blocked.
-> The operating system's **scheduler** takes care of blocking and unblocking the thread, ensuring it doesn’t waste CPU resources.

2. **Signal operation:**
Syntax: `sem_post(sem_t *S)`
Definition:
```c
sem_post(sem_t *S)
{
	//freeing whatever resource was being used
	S++;
}
```
- Signal tells other processes that a resource is freed.

3. **Initialize semaphore**:
Syntax: `sem_init(sem_t *S, int pshared, unsigned int value)`
1. `int pshared` determines whether the semaphore is shared only *within a process* (i.e among threads of a process) or *between* processes.
	- if `pshared = 0` -> semaphore is only within a process. Used for **thread synchronization**.
	- if `pshared = 1` -> semaphore is shared between different processes. Used for **process synchronization**. Semaphore is stored in shared memory to allow other processes to access it.
2. `unsigned int value` Initializes the value stored by semaphore. Indicates the amount of resources available
	- if `value > 0` : Multiple instances of resources are available for use
	- if `value = 0`: No resources are available. Processes busy wait, or are blocked until resource frees up.
1. `sem_t *S` Pointer to the semaphore that has to be initialized. Semaphore is stored and represented by the variable

### 1.1. Semaphore Implementation as structure
Semaphores can be implemented as a structure to enable process suspension/blocking instead of busy waiting
```c
typedef struct {
	int value;
	struct process *list; //struct process just stores information about a process like pthread_t, process name, et.c
} semaphore;
```

We implement `wait()`, `signal()` as
```c
wait(semaphore *S)
{
	S->value--;
	if(S->value < 0)
	{
		//Add process P to suspended/blocked S->list
		sleep();
	}
}

signal(semaphore *S)
{
	S->value++;
	if(S->value <= 0)
	{
		//remove process P from S->list
		wakeup(P);
	}
}
```


> See Further: `compare_and_swap()`, spinlocks (in mutex locks)