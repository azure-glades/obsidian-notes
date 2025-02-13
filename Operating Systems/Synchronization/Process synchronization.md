When multiple processes require a resource, it is important to ensure all processes receive the most up-to-date version of that resource. 
- This is possible by sharing the resources between all processes and making them access the same copy. 
- In some cases the resources cannot be shared and we need to create multiple copies that are continuously synced with each other to ensure changes are made across all copies
Both of these introduce uncertainties where changes may be done to the same segment of the resource concurrently, or where the resource is not properly updated before processes access the resource. This introduces the need for sync between processes where processes communicate with each other to ensure the shared resource is kept synced.
- This is called the critical section problem, and it is solved by various implementations of synchronization locks
A lack of synchronization causes *race conditions* and *[[Deadlocks]]*
## [[Critical-Section Problems]]
- The **critical section problem** is the violation of data integrity and consistency in a shared resource caused due to multiple processes concurrently accessing and modifying the resource.
- A **critical section** refers to a segment of code that accesses or modifies shared resources, such as variables or files. To ensure data integrity and consistency, it is essential that only one process can execute within its critical section at any given time.

It's conditions of the critical section problem are:
-  **Mutual Exclusion**: This condition ensures that if one process is executing in its critical section, no other process can enter its critical section. 
	- This prevents simultaneous access to shared resources, thereby avoiding conflicts and potential data corruption
	
- **Progress**: If the critical section is not being access by a process, then *only* the other waiting processes can *decide* which process should next enter the critical section
	- The decision about which process can enter the critical section should not be postponed indefinitely
	
- **Bounded Waiting**: There is a limit on how many times *other* processes can enter their critical sections *after* a *request* has been made by a waiting process. 
	- This prevents *starvation*, where a process could be indefinitely delayed from entering its critical section due to continuous access by other processes.

The critical section problem highlights the need for synchronization mechanisms in concurrent programming
Example: If two processes attempt to modify a shared variable simultaneously, the final value may be inconsistent or incorrect (formally called a *race condition*)


> [!info]+ Race Condition
>- When several processes access and manipulate the same data concurrently and the outcome of the execution depends on the particular order in which the access takes place, is called a race condition.
>- This order of access is completely random resulting in arbitrary results.
> - Characteristics:
> 	- **Non-Determinacy**: The same program may exhibit different behaviors depending on how threads are scheduled and executed, leading to bugs that are difficult to reproduce and fix.
> 	- **Synchronization Issues**: Race conditions typically arise in scenarios where proper synchronization mechanisms (like locks or semaphores) are not implemented, allowing concurrent access to shared data
## Solutions to Critical-Section Problems
### 1. [[Peterson's Solution]]
- `flag` : stores whether a process needs to run critical section
- `turn`: stores the ID of the process currently running in critical section

A process runs the entry section _atomically_ (i.e process cannot be preempted when in entry section)
> [!info]- Atomic (Indivisible)
> An instruction that cannot be divided/interrupted

> How will a program know its in critical section? What if it doesnt tell the OS its in critical section?
> Who is determining the how the processes run?
> single core can execute only 1 process at a time. Where can resource conflicts occur here?
### 2. [[Synchronization Hardware]]
Peterson's algorithm is a software-based solution for resource synchronization. There are hardware solutions to synchronization hardware, like:
- Memory barriers: Block the access of same address of memory simultaneously by different processors
- Hardware instructions: Low level operations for atomic manipulation of memory
- Atomic Variables: Variables who's manipulation and access occurs atomically and in-sequence
**Kernel Construct**: API Tool provided by OS for communication, sychronization and concurrency
### 3. [[Mutex Locks]]
A mutex lock is a high-level software tool to allow application designers to solve critical section problems by mutual exclusion.
- A process must acquire a mutex lock before entering critical section
- A process must release a mutex lock before entering remainder section

>[!info]+ Busy waiting
>**Busy waiting**, also known as **spinning** or **busy looping**, is a synchronization technique in operating systems where a process repeatedly checks for a condition to be met before proceeding with its execution.
>- This often decreases CPU efficiency since CPU cycles are spent to check the access condition
>- This is avoided by process blocking
### 4. [[Semaphore]]
A **semaphore** is a synchronization primitive type (in `semaphore.h` header) used in to manage access to shared resource
- It helps ensure proper coordination between threads
- preventing race conditions 
- maintaining mutual exclusion

>See further: Kernel construct, Interprocess communication - Message queues, mailbox and pipes
### Difference between mutex and semaphore

| Feature             | Mutex                                        | Semaphore                                           |
| ------------------- | -------------------------------------------- | --------------------------------------------------- |
| **Mechanism**       | Locking Mechanism                            | Signaling Mechanism                                 |
| **Nature**          | Object                                       | Integer Variable                                    |
| **Modification**    | Modified only by the owning process          | Modified by any process using `wait()`/`signal()`   |
| **Resource Access** | Exclusive access to a single shared resource | Controls access to multiple instances of a resource |
| **Ownership**       | Owned by the acquiring thread/process        | No ownership; signaling is key                      |
| **Types**           | No subtypes                                  | Counting and Binary                                 |
| **Operation**       | Lock/Unlock                                  | Wait (Decrement)/Signal (Increment)                 |
| **Purpose**         | Protecting critical sections                 | Controlling access to shared resources              |
