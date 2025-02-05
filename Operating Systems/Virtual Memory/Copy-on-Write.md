**Definition:**
	Memory management technique where multiple processes share the same memory pages until one of them modifies a page. When a modification is done, the system duplicates/copies the page and is assigned exclusively to the modifying process while the other processes continue to share the original page
	- Most commonly done among parent and child processes


- The `fork()` system call is used to create a new process (the child) by duplicating the existing process (the parent).
	- With COW both processes initially share the same memory pages. These pages are marked as read-only and are called *copy-on-write pages*.
	- If either process attempts to modify a shared page, a page fault occurs, triggering the COW mechanism. Copy is made and access is given to that process

- Since most child processes are assigned different tasks via `execl()` there is no point in immediately creating copies of the parent pages for the child (when `fork()` is called). The OS avoids this overhead by sharing pages
	- Hence, only when the child requests/*writes* onto the shared page like calling `exec()` the page is copied and assigned to the child process and frames are mapped.
	- This prevents shared but unmodified pages from being translated/mapped and saves a huge CPU overhead.

- The `vfork()` system call is similar to `fork()`, but it is optimized for scenarios where the child process will immediately call `exec()` without modifying the parent.
	- With `vfork()`, the parent is suspended and the child gets access to its page (no page sharing/COW)
	- If the child does any modifications to the page, it causes undefined behaviour.
	- Hence, `vfork()` is only used when we are certain that the child immediately calls `exec()`. It avoids the overhead involved with defining COW pages and sharing them.
![[Pasted image 20241231171807.png]]
![[Pasted image 20241231171814.png]]

