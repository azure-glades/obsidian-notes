A mutex lock is a bit of software that locks the usage of shared resources when a thread is running its critical section. It's a bit of software designed by OS designers to enable high-level application programmers to implement solutions to critical section problems.
- It contains a `available` variable which indicates if a resource is available or not.
- The `acquire()` function is used to check if it is available and acquire the lock
- The `release()` function is used to release the lock and inform other processes that the resource is available

## Implementation
*Definition of `acquire()`*
```c
acquire() {
while (!available){
	 /* busy wait */ 
}
available = false;
}
```
*Definition of `release()`*
```c
release() {
	available = true;
}
```

- These functions have to run atomically and are often implemented with `compare_and_swap()` kernel functions
- The main disadvantage is **busy waiting** which has a tendency to consume and waste CPU cycles
- It takes away cycle time from other processes that may use it efficiently. One solution, also implemented in semaphores is [[Process Blocking]] where the process waits for an event (lock to be released) to occur without consuming CPU time
	- This is also implemented in semaphores

This type of mutex locks (that cause busy-waiting) do have advantages. They are termed **Spin Locks**
> [!info] **Spin Lock**
>  Unlike traditional locks that may put a thread to sleep while waiting for a resource, a spin lock causes the thread to repeatedly checking if the lock is available, effectively it "spins" in a loop.

## Key Features of Spin Locks
- **Busy Waiting**: When a thread attempts to acquire a spin lock that is already held by another thread, it enters a busy-wait state, continuously checking the lock's status until it becomes available. 
	- This is referred to as "spinning" because the thread is actively using CPU cycles while waiting, rather than being put to sleep
- **Low Overhead**: Spin locks are often used in scenarios where the expected wait time for acquiring the lock is very short. 
	- They avoid the overhead of blocking and waking up threads,
	- This makes the suitable in high-performance computing environments (like multi-core systems) where threads can run on different processors
- **Non-blocking**: Unlike mutexes or semaphores that may block a thread and switch its context out, spin locks keep the thread in a runnable state, allowing it to immediately resume execution once the lock is acquired. 
	- They perform better in cases where there is a lot of blocking-unblocking and resource switching occurring

### 2.1. When a Process "Spins"
When we say that a process "spins," it means that the process is actively waiting in a loop for a condition to change—specifically, for the spin lock to become available. During this time, the process does not perform any useful work; instead, it consumes CPU resources by repeatedly checking whether it can acquire the lock. 
- This behavior can lead to inefficiencies if many threads are spinning on the same lock, as they waste CPU cycles that could be used for other tasks

## Advantages and Disadvantages
### Advantages:
- **Performance**: Spin locks can provide better performance than blocking locks in scenarios with short wait times.
- **Simplicity**: Their implementation is straightforward compared to more complex locking mechanisms.
### Disadvantages:
- **CPU Utilization**: They can waste CPU cycles if the wait time is long, as they keep checking the lock rather than yielding control.
- **Not Suitable for Long Waits**: If many threads are competing for a spin lock and the critical section is held for an extended period, this can lead to significant performance degradation.