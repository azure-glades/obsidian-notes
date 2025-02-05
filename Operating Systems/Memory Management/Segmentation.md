*Definition:*
	Segmentation is a memory management technique used in operating systems that divides a computer's primary memory into variable-sized segments. Each segment represents a logical unit of a program, such as functions, data structures, or objects, allowing for more intuitive organization compared to fixed-size paging systems.
- Segmentation involves dividing memory into different segments, each with specific permissions (read, write, execute)
- when a program attempts to access a memory segment that it is not allowed to access, a ***segmentation fault*** occurs
A logical address space is a collection of segments
![[Pasted image 20250201225143.png]]
- **Variable-Sized Segments**: Unlike paging, which divides memory into fixed-size pages, segmentation allows segments to vary in size based on the logical structure of the program.
	- This means that related functions or data can be grouped together within the same segment, enhancing both performance and organization
- **Logical Addressing**: In segmentation, a logical address consists of two parts: a segment number and an offset within that segment.
	- This structure allows the operating system to translate logical addresses into physical addresses by adding the segment's base address to the offset

| Feature                | Segmentation                          | Paging                               |
|------------------------|--------------------------------------|-------------------------------------|
| Size                   | Variable-sized segments               | Fixed-size pages                    |
| Address Structure      | Segment number + offset               | Page number + offset                |
| Memory Allocation      | Non-contiguous allocation             | Allocated as whole units            |
| Fragmentation          | External fragmentation possible       | Internal fragmentation possible      |
| Complexity             | More complex address translation      | Simpler address translation          |
- Segmentation avoids internal fragmentation but cannot prevent external fragmentation (which is the exact opposite of paging, which avoids external fragmentation but cannot prevent internal fragmentation)

## Segment Table
All segments of memory are stored in a *segment table*.
- Each entry has a *segment base address* and *segment limit address*

![[Pasted image 20250201225634.png]]

## Advantages of Segmentation

- **Logical Grouping**: Segmentation facilitates logical grouping of related data and functions, making it easier for programmers to understand and manage memory usage
- **Protection and Sharing**: Each segment can have different protection attributes (e.g., read-only or read-write), allowing for better isolation between processes. Additionally, segments can be shared among processes without duplicating data in memory
- **Reduced Internal Fragmentation**: Since segments can be of varying sizes, segmentation minimizes internal fragmentation compared to fixed-size pages, where unused space within pages can lead to wasted memory.
## Disadvantages of Segmentation
- **External Fragmentation**: One significant downside is external fragmentation, which can occur when free memory is divided into small blocks that are not contiguous enough to satisfy segment requests
- **Complex Address Translation**: The process of translating logical addresses into physical addresses is more complex in segmentation than in paging. It typically involves multiple table lookups, which can increase overhead and reduce performance