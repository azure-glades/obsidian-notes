- **Definition**: Suspending/Swapping a process involves temporarily halting its execution and moving it out of the main memory, often into secondary storage (disk). This is done to free up resources or manage memory more efficiently.
	- The swapped/suspended process is stored in the *suspend queue*
- **State**: A suspended process is neither running nor ready; it may be in a suspended blocked state (waiting for an event while being swapped out) or suspended ready state (not currently eligible for execution but not waiting for any event).
- **Example**: If the operating system needs to free up memory and there are processes that are not currently active, it may suspend these processes by moving them to disk.

| Aspect                  | Blocking a Process                                  | Making a Process Wait                             | Suspending a Process                               |
|-------------------------|----------------------------------------------------|--------------------------------------------------|---------------------------------------------------|
| Definition              | Waiting for an event/resource to become available  | General term for halting execution until conditions are met | Temporarily halting execution and possibly moving to disk |
| State                   | Blocked state                                      | Can lead to blocked or suspended states          | Suspended state (may be in secondary storage)     |
| Resource Management      | Does not free up memory                            | May or may not involve resource management       | Frees up memory by moving processes out of RAM     |
| Examples                | Waiting for I/O completion                          | Waiting on locks or conditions                    | Swapping out inactive processes for efficiency     |
