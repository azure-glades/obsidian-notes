Thread libraries are APIs used by the programmer to create and manage threads. Thread libraries can be implemented in user-space or kernel-space
- If the entire library is in user-space, all library functions server as local function calls in the user space which are interfaced with the kernel internally
- If it is a kernel-level library, all code and data structures of the library reside in the kernel space and all library functions are invoked by *system calls*

There are 3 main thread libraries:
- POSIX pthreads
- Windows threads
- Java threads
	- POSIX pthreads have user-level and kernel level implementations
	- Java threads run on the JVM and have to be interfaced to the host OS via respective thread-APIs
>[!INFO]+ **POSIX**
>POSIX, which stands for **Portable Operating System Interface**, is a set of standards specified by the IEEE to standardize APIs, command-line shells, and interfaces across different operating systems
>- This allow software to be seamlessly ported between POSIX-compliant OSes easily
>- pthreads is a thread-library library seen in UNIX which adheres to the POSIX standard

### Ways of creating threads
- **Asynchronous threading**: When parent and child threads execute concurrently and independently. (Parent can die before child and leave orphans)
	- No data sharing between them
- **Synchronous threading**: When parent creates child threads which run in parallel while the parent remains in waiting state for the child threads to terminate.
	- Lots of data sharing and synchronisation exists between child threads.

## POSIX pthreads
POSIX is a set of standards for thread behaviour. it is implemented via pthreads library included by `#include <pthread.h>`
Thread IDs are their own data-type called `pthread_t`
- threads made by `pthread_create()`
- threads terminate with `pthread_join()`
- thread attributes initialized via `pthread_attr_init()`

>[!IMPORTANT] **Thread Pools**
> A thread pool is a set of pre-initialized, unmapped threads that are called upon by process. Thread pools save a lot of overhead since new threads need not be created, instead threads from the pool can be mapped to the system call.
> - Once a thread completes execution, it is returned to the thread pool.
> - If the pool is empty, the task waits until a thread is freed up-> This saves a lot of initial overhead in creating and allocating threads.
## Windows threads
Windows thread library is used with `#include <windows.h>` and contain a similar set of essential thread management functions.
Thread IDs are defined with `DWORD`
- threads made by `CreateThread()`
- threads terminate with `WaitForSingleObject()`
	- For multiple threads it is `WaitForMultipleObjects()`

## Java Threads
Threads are an essential part in Java and are run completely on the JVM. The JVM translates these thread function calls to system calls for the OS on the fly.
Threads are created by *implementing the `Runnable` interface*, or by *extending the `Thread` class*.
- Objects are made under this class, and called with the `thread.start()` which calls the `run()` method on our behalf
- Threads are terminated by `thread.join()`
