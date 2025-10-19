***A thread is the most basic unit of execution. Processes can be single-threaded, or they can be multi-threaded***
- Threads are the smallest self-contained units of execution that a scheduler can schedule. All processes are executed as threads; either in a single thread or divide across multiple threads
Each core in a CPU can process 2 threads at a time.
- There is **parallel processing** between cores of a cpu, since the CPU can run different threads of different cores in parallel 
- There is **concurrent processing** within a cpu since the 2 threads compete for execution time in a single core
> [!NOTE] **Types of Parallelism**
> - *Data parallelism*: Allocating bits of data to multiple threads. (EX: Array can be divided across 2 threads)	
> - *Task parallelism*: Distributing tasks of a process (as threads) across cores
Multi-threading is used to take advantage of multi-core CPU architectures

> A concurrent system supports more than one task by allowing all the tasks to make progress. In contrast, a parallel system can perform more than one task simultaneously. Thus, it is possible to have concurrency without parallelism.
-> [[Thread Libraries]]
## Threads
A **thread** of [execution](https://en.wikipedia.org/wiki/Execution_\(computing\) "Execution (computing)") is the smallest sequence of programmed instructions that can be managed independently by a [scheduler](https://en.wikipedia.org/wiki/Scheduling_\(computing\) "Scheduling (computing)") 
- A thread is a component of a process
- Consists of a program counter, a stack, a set of registers, and a thread ID.
- Made at run-time by the process itself. Since the process creates and divides its allocated registers+stack+program-counter, there is less overhead to the CPU for thread creation (that compared to process creation, i.e forking)

![[Pasted image 20241023000101.png]]
### Types of threads
- **User-Level Threads**: These are managed by user-level libraries and are not recognized by the operating system kernel. They are faster to create and manage but can block the entire process if one thread performs a blocking operation
	- When a user thread does a system-call, it's mode of execution changes. The system-call gains `sudo` permissions and executes in kernel mode. Once the system-call is returned, the thread looses its `sudo` permissions and returns to user mode execution
- **Kernel-Level Threads**: These are managed directly by the operating system kernel. The kernel is aware of these threads, which allows for better scheduling and management but incurs more overhead compared to user-level threads
> [!important] **Amdahl's Law**
> Amdahl’s Law is a formula that identifies potential performance gains from adding additional computing cores to an application that has both serial (nonparallel) and parallel components.
> - If a task has components that can be run in parallel, it gains a bigger performance increase due to multi-threading $$\text{speedup} \le \frac{1}{S + \frac{1-S}{N}}$$
> Where $S$ is the portion that must be done serially and $1- S$ is the portion that can be parallelized. $N$ is the number of cores utilized.
> Ex:
> - If S = 1, then speedup = 1, i.e there is no speedup
> - If S = 0, then speedup = N -> Process can be done N times faster (or in N times less time) i.e more number of cores, more is the speedup
> - If parallel part = 75%, then S = 0.25. speedup = 1.6 if there are 2 cores. and speedup is 2.28 if there are 4 corest
> As $N \rightarrow \infty$ then $\text{speedup} \rightarrow 1/S$ 
> - Suppose S = 50%, then the theoretical maximum speed up (when N = $\infty$) is 2
> 
> 
## Multi-threading models
A model that is used to map user threads to kernel threads. User threads are supported above the kernel and are managed without kernel support, whereas kernel threads are supported and managed directly by the operating system.

>*Why is there a need for mapping user to kernel threads?*
>Kernel threads are the actual entities that the operating system schedules for execution on the CPU. While user threads are managed by user-level libraries, they cannot execute independently without being associated with a kernel thread
>- This is because the kernel manages and allocates resources only to kernel threads. The scheduler only views kernel threads as valid tasks and cannot schedule user threads

1. **Many-to-one**:
	- Multiple user-threads are mapped to a single-kernel thread.
	- Multiple threads may not run in parallel in multi-core systems because they are mapped to only 1 executing kernel thread.
	- If kernel-thread is blocked all mapped threads get blocked
	- Used by *GNU portable threads, Solaris green threads*
![[Pasted image 20250201212023.png]]

2. **One-to-one**:
	- Each user-thread is mapped to a single kernel-thread.
	- Number of threads per process is restricted to prevent task overloading
	- Allows for complete paralellism
![[Pasted image 20250201212043.png]]

1. **Many-to-many**:
	- Allows many user threads to be assigned to different multiple kernel threads. Assignment is implementation dependant
	- EX: *Windows threadfibre library*
![[Pasted image 20250201212100.png]]
## Benefits of Multi-threading
- **Responsiveness**: Multi-threading in interactive applications allows for 1 thread to look for GUI inputs while other threads perform tasks. Since there is a thread always listening for user-input, there is better responsiveness
- **Resource sharing**: Multi-threading allows for better distribution and allocation of resources for a process. 
	- Threads of a process share code, data, files and memory. Hence new memory need not be allocated and files need not be copied.
- **Economy:** Since threads share memory and code, it is much faster to create more threads than processes
	- It is *quicker to context-switch between threads,* than between processes.
- **Scalability:** Enables complete utilisation of multi-core systems. Enables multiple processes to be run across cores, or to run a single process quicker by dividing the work between cores. 
	- Single-threaded processes can only run on 1 core, and cannot utilise the power of clustered systems. 
- **Multicore/multiprocessor** systems have multiple CPU capable of execution. Causes complexity of code
	- *Master-slave schedulers.* Master scheduler overtakes task assignment. Slave schedulers deal with scheduling individual cores. Implementation dependant
>[!INFO]+ **Multicore systems**
>Computer systems that have multiple processing cores within a single chip
>*Multi-threaded programming* developed as a technique to better utilize multi-core systems
## Challenges of multi-threading
- Identifying tasks that can be split across threads
- Balancing the number of parallel threads to prevent high cpu overheads which slows down processing
- Data has to be split so that it can be handled by different threads. This data has to be stored on the respc L1 caches of the cores running the threads
- Dependency of data between two threads must be analyzed so that the order of execution of certain tasks is synchronized. A thread requiring data from another task cannot execute until it has received the relevant data
- Access of common pools of data has to be synchronized across threads.
- Testing and debugging is a lot harder since multiple execution paths are possible.
