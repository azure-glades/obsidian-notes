- **Definition**: A process is said to be blocked when it cannot continue its execution because it is waiting for some event to occur, typically an I/O operation or the availability of a resource (like a *synchronization lock*).
- **State**: In this state, the process is moved from the running state to the blocked state. It will remain in this state until the event it is waiting for occurs (e.g., data becomes available).
- **Example**: If a process attempts to read from a disk and the data is not yet available, it will enter a blocked state until the disk read operation completes.

| Aspect                  | Blocking a Process                                  | Making a Process Wait                             | Suspending a Process                               |
|-------------------------|----------------------------------------------------|--------------------------------------------------|---------------------------------------------------|
| Definition              | Waiting for an event/resource to become available  | General term for halting execution until conditions are met | Temporarily halting execution and possibly moving to disk |
| State                   | Blocked state                                      | Can lead to blocked or suspended states          | Suspended state (may be in secondary storage)     |
| Resource Management      | Does not free up memory                            | May or may not involve resource management       | Frees up memory by moving processes out of RAM     |
| Examples                | Waiting for I/O completion                          | Waiting on locks or conditions                    | Swapping out inactive processes for efficiency     |
