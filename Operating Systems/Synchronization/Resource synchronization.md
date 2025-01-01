- A way to share resources among processes without causing conflicts
- There are physical resources and software resources.
- Not all resources can be concurrently accessed and manipulated by multiple resources

## 1. Critical-Section Problems
- The **critical section problem** is a fundamental issue in concurrent programming and operating systems, arising when multiple processes or threads attempt to access shared resources simultaneously. 
- A **critical section** refers to a segment of code where shared resources, such as variables or files, are accessed and modified. To prevent inconsistencies and ensure data integrity, it is essential that only one process can execute within its critical section at any given time.

It's conditions are:
-  **Mutual Exclusion**: This condition ensures that if one process is executing in its critical section, no other process can enter its critical section. 
	- This prevents simultaneous access to shared resources, thereby avoiding conflicts and potential data corruption
	
- **Progress**: When no process is currently executing in its critical section, and there exists a process that wishes to enter it, the system must ensure that this process is not kept *waiting indefinitely*. 
	- The decision about which process can enter the critical section should not be postponed indefinitely
	
- **Bounded Waiting**: This condition stipulates that there must be a limit on how many times other processes can enter their critical sections after a request has been made by a waiting process. 
	- This prevents *starvation*, where a process could be indefinitely delayed from entering its critical section due to continuous access by other processes.

The critical section problem highlights the need for synchronization mechanisms in concurrent programming
Example: If two processes attempt to modify a shared variable simultaneously, the final value may be inconsistent or incorrect (formally called a *race condition*)

> [!info]+ Race Condition
>-  A race condition occurs when two or more threads access a shared resource (such as a variable in memory) and the outcome of their execution depends only on the order of their accesses/execution. 
> - The order of execution/access is arbitrary, and can vary between different executions of the program, leading to different results. 
> This random behaviour is a cause of bugs and critical faults
> - Characteristics:
> 	- **Non-Determinacy**: The same program may exhibit different behaviors depending on how threads are scheduled and executed, leading to bugs that are difficult to reproduce and fix.
> 	- **Synchronization Issues**: Race conditions typically arise in scenarios where proper synchronization mechanisms (like locks or semaphores) are not implemented, allowing concurrent access to shared data

### 1.1. [[Producer-Consumer Problem]]/ Bounded-Buffer Problem
### 1.2. [[Dining Philosopher Problem]]
### 1.3. [[Reader Writer Problem]]

## 2. Solutions to Critical-Section Problems
### 2.1. [[Peterson's Solution]]
- `flag` : stores whether a process needs to run critical section
- `turn`: stores the ID of the process currently running in critical section

A process runs the entry section _atomically_ (i.e process cannot be preempted when in entry section)
> [!info]- Atomic (Indivisible)
> An instruction that cannot be divided/interrupted

> How will a program know its in critical section? What if it doesnt tell the OS its in critical section?
> Who is determining the how the processes run?
> 1 core can execute only 1 process at a time. Where can resource conflicts occur here?
### 2.2. [[Synchronization Hardware]]
Peterson's algorithm is a software-based solution for resource synchronization. There are hardware solutions to synchronization hardware, like:
+
- Memory barriers: Block the access of same address of memory simultaneously by different processors
- Hardware instructions: Low level operations for atomic manipulation of memory
- Atomic Variables: Variables who's manipulation and access occurs atomically and in-sequence
**Kernel Construct**: API Tool provided by OS for communication, sychronization and concurrency

### 2.3. [[Mutex Locks]]
A mutex lock is a high-level software tool to allow application designers to solve critical section problems by mutual exclusion.
- A process must acquire a mutex lock before entering critical section
- A process must release a mutex lock before entering remainder section

>[!info]+ Busy waiting
>**Busy waiting**, also known as **spinning** or **busy looping**, is a synchronization technique in operating systems where a process repeatedly checks for a condition to be met before proceeding with its execution.
>- This often decreases CPU efficiency since CPU cycles are spent to check the access condition
>- This is avoided by process blocking
### 2.4. [[Semaphore]]
A+ **semaphore** is a synchronization primitive type (in `semaphore.h` header) used in to manage access to shared resource
- It helps ensure proper coordination between threads
- preventing race conditions 
- maintaining mutual exclusion

>See further: Kernel construct, Interprocess communication - Message queues, mailbox and pipes