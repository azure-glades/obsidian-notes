Page tables are structured in different manners to solve different problems

### 1. Hierarchical Page Tables
- Multiple levels of page tables -> page tables to store page tables
- Addresses have outer page base - offset registers used by outer page tables to be diverted to inner page tables which store pointers to frames in memory. 
- **Logical address:** page indexes of all outer and inner page tables + page offset for the innermost table. Used by the page tables to direct to the correct inner page tables storing the base-limit registers (of the physical address)![[Pasted image 20241231153751.png]]
- Also called *forward mapping* because address translation occurs from outer to inward tables
![[Pasted image 20241231153634.png]]

- **Disadvantage**:
	- Wastage of memory in storing and recalling these page tables and their pointers
	- High memory addressing times since multiple tables (and hence memory accesses have to be done)

>[!info] **64-bit systems**
>Hierarchical paging is impractical in 64-bit systems due to the sheer amount of address spaces
> Suppose a 64-bit address is divided as such: (42 + 10 + 12 = 64)
> 	first 42 bits -> outer page table
> 	next 10 bits -> inner page table
> 	last 12 bits -> page offset (Each page is 4 KB = $2^{12}$)
> This means there are $2^{42}$ possible entries for the outer page table (which is around 400GB, just to index the available memory)
> Even if we divide it further into 2nd outer table
> 	first 32 bits -> 2nd outer page table
> 	next 10 bits -> 1st outer page table
> 	next 10 bits -> inner page table
> 	last 12 bits -> page offset (4 KB)
> Outer page table is still 16 GB in size. Only way to fix this is adding more page tables
---
### 2. Hashed Page Tables
Hashing is used to read addresses and store pages in a page table. Generally, linked list hashing is used to avoid collisions. 
- **Logical address:** Virtual page number + Page frame offset (*Virtual page number is used as a key to the hash function*)
- **Physical address:** Usual base-limit registers. Hash table stores the appropriate base register of the frame ![[Pasted image 20241231155346.png]]

> [!NOTE]+ Clustered page tables
> Each entry in hash table refers to multiple pages instead of 1
> This allows a single entry to refer to multiple physical frames.
> - Particularly useful for *sparse address spaces* since a lot of empty memory need not receive its own entry on the page table
---
### 3. Inverted Page Tables
Usually, each process has its own page table that it uses to lookup and access memory that is allocated to it. Due to virtualization, a lot of pages are shared across processes, and hence these pages repeat over their respc page tables. This balloons the amount of memory occupied by the page tables for a process
- Inverted page tables are a single system-wide page table that locates all pages to their frames and the process id that the page is assigned to
- *Logical address:* process id + page number + page offset
- **Disadvantage:**
	- It takes a long amount of time to match a pid and find its page (solved by using hashing to store the pids)
	- Does not allow page sharing since only a single virtual address can be mapped to a pid and page number
![[Pasted image 20241231162226.png]]

