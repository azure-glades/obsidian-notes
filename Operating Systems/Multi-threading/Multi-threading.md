***A thread is a portion of a process that executes. Processes can be single-threaded, or they can be multi-threaded***
[[Process Waiting]]

Each core in a CPU can process 2 threads at a time.
- There is **parallel processing** between cores of a cpu, since the CPU can run different threads of different cores in parallel 
- There is **concurrent processing** within a cpu since the 2 threads compete for execution time

Multi-threading is used to take advantage of multi-core CPU architectures
- Allows for parallel execution of code through threads
- Threads can be made at runtime
- Threads are made by the process itself, and the order of creation of threads is determined by the process, giving less overhead to a cpu (thread creation is faster than process creation)
![[Pasted image 20241023000101.png]]
## 1.1. Benefits of Multi-threading
- **Responsiveness**: Multi-threading in interactive applications allows for 1 thread to look for GUI inputs while other threads perform tasks. Since there is a thread always listening for user-input, there is better responsiveness
- **Resource sharing**: Multi-threading allows for better distribution and allocation of resources for a process. 
	- Threads of a process share code, data, files and memory. Hence new memory need not be allocated and files need not be copied.
- **Economy:** Since threads share memory and code, it is much faster to create more threads than processes
	- It is *quicker to context-switch between threads,* than between processes.
- **Scalability:** Enables complete utilisation of multi-core systems. Enables multiple processes to be run across cores, or to run a single process quicker by dividing the work between cores. 
	- Single-threaded processes can only run on 1 core, and cannot utilise the power of clustered systems. 
- **Multicore/multiprocessor** systems have multiple CPU capable of execution. Causes complexity of code
	- Master-slave schedulers. Master scheduler overtakes task assignment. Slave schedulers deal with scheduling individual cores. Implementation dependant
## 1.2. Challenges of multi-threading
- Identifying tasks that can be split across threads
- Balancing the number of parallel threads to prevent high cpu overheads which slows down processing
- Data accessed by threads has to be accessed by respc cores, and have to be kept on relevant L1 cache
- Access of common pools of data has to be synchronized across threads.
- Testing and debugging is a lot harder.

> [!NOTE]
> ### Parallelism
> - *Data parallelism*: Allocating bits of data to multiple threads. (EX: Array can be divided across 2 threads)	
> - *Task parallelism*: Distributing tasks of a process (as threads) across cores

---
## 1.3. Multi-threading models
- **Many-to-one**:
	- Multiple user-threads are mapped to a single-kernel thread.
	- Multiple threads may not run parallely in multi-core systems because they are mapped to only 1 executing kernel thread.
	- If kernel-thread is blocked all mapped threads get blocked
	- Used by *GNU portable threads, Solaris green threads*
- **One-to-one**:
	- Each user-thread is mapped to a single kernel-thread.
	- Number of threads per process is restricted to prevent task overloading
	- Allows for complete paralellism
- **Many-to-many**:
	- Allows many user threads to be assigned to different multiple kernel threads. Assignment is implementation dependant
	- EX: *Windows threadfibre library*



> [!NOTE] 
> ## Amdahl's Law
> Measures the performance gain from adding extra cores to an application with serial and parallel processing threads.
> - Predict the theoretical speedup when using multiple processors for a given application
> ![[Pasted image 20241023001134.png]]
> Here, 
> 	S is portion of applications that must run serially
> 	N is the number of processing cores
> As N -> $\infty$ , speedup -> $\frac{1}{S}$ 

---
## 1.4. Thread libraries
Thread libraries are APIs used by the programmer to create threads and split them across processes. Consists of libraries with functions used in managing threads.
- POSIX pthreads
- Windows threads
- Java threads
	- POSIX pthreads have user-level and kernel level implementations
	- Java threads run on the JVM and have to be interfaced to the host OS via respective thread-APIs

- **Asynchronous threading**: When parent and child threads execute concurrently and independently. (Parent can die before child and leave orphans)
	- No data sharing between them
- **Synchronous threading**: When parent creates child threads which run in parallel while the parent remains in waiting state for the child threads to terminate.
	- Lots of data sharing and synchronisation exists between child threads.

### 1.4.1. POSIX pthreads
POSIX is a set of standards for thread behaviour. it is implemented via pthreads.
- threads made by `pthread_create()`
- threads terminate with `pthread_exit()`
	- child threads terminate with `pthread_join()`
- thread attributes initialized via `pthread_attr_init()`
### 1.4.2. Thread Pool
- A collection of ready-state threads that can take up a process.
- Prevents the CPU from being interrupted for thread-allocation
- Executed threads are returned back to the pool for re-allocation to another process
