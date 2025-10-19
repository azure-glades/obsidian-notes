**Deadlock** is a situation where a group of processes is stuck in a state where they are unable to proceed because each one is waiting for a resource held by another process.
## Coffman's conditions:
4 possible situations can cause deadlocks:
1. **Mutual Exclusion**: When multiple processes are trying to access a resource that cannot be shared.
2. **Resource holding/Hold and wait**: A process is holding a resource and is waiting for additional resources that are not available (probably because they are held by other processes).
3. **No preemption**: A resource cannot be forcibly taken away from a process and other dependant processes have to wait for the process to voluntarily release the resource.
4. **Circular dependency**: There are a chain of processes waiting to use the resource held by the next process in the chain.
