- Linux is a monolithic kernel
- Linux considers everything as a file
	- File extension does not matter
	- Files have stats, access priviledges etc
	- All files are accessed in the form of streams
- Max file size is 128 TB

- A structured collection of files is a file system
	- Cluster filesystem
	- Network filesystem
Example: NTFS, EXFAT, FAT32, EXT4

- objects
	- file
	- inode
	- dentry
	- superblock


- virtual file system is a layer in the kernel file management
	- proc file system
	- pseudo file system
	- swap file system

- mounting: attaching another file system at a location in the root file system
- formating: a process of creating a file system

- Superblock: structure representing an instance of a file-system
- Inode: Index node -> exists for every object in a file system. To index files in a file system
- dentry: directory entry 
check `glibc` for structs of superblock, inode, etc
`fsync`
`flock`


-> AI generated
## Linux Kernel Architecture

### Monolithic Kernel
- **Definition**: Linux is classified as a **monolithic kernel**, meaning the entire operating system runs in kernel mode, allowing direct interaction between various components without the need for inter-process communication (IPC) mechanisms. This design choice enhances performance and simplifies development[1][4].
- **Components**: All essential services such as file management, memory management, device drivers, and process management are integrated into a single large binary, enabling efficient execution of system calls[3][9].

### Everything is a File
- **Concept**: In Linux, everything is treated as a file, including programs, directories, block devices, and character devices. This abstraction allows users to interact with system components uniformly[2][6].
- **File Characteristics**:
  - **File Extensions**: The extension of a file does not affect its functionality within the system.
  - **File Attributes**: Files possess attributes such as statistics (size, modification time) and access privileges (read/write permissions).
  - **Stream Access**: All files are accessed in the form of streams, facilitating data manipulation and transfer.

### File System Structure
- **Definition**: A file system is a structured collection of files that organizes how data is stored and retrieved.
- **Types of File Systems**:
  - **Cluster File System**: Manages storage across multiple nodes.
  - **Network File System**: Allows access to files over a network.
- **Examples**: Common file systems include NTFS, EXFAT, FAT32, and EXT4.

### Objects in the File System
- **File**: The basic unit of storage that contains data.
- **Inode**: An index node that stores metadata about files (e.g., ownership, permissions).
- **Dentry**: A directory entry that links filenames to their respective inodes.
- **Superblock**: A structure representing an instance of a file system, containing information about the file system's size, status, and location.

### Virtual File System (VFS)
- **Purpose**: VFS acts as an abstraction layer in kernel file management, allowing different file systems to be accessed uniformly.
- **Types of Virtual File Systems**:
  - **Proc File System**: Provides an interface to kernel data structures.
  - **Pseudo File System**: Represents data structures that do not correspond to physical files.
  - **Swap File System**: Manages swap space for virtual memory.

### Mounting and Formatting
- **Mounting**: The process of attaching another file system at a specific location in the root file system. This allows users to access multiple file systems seamlessly.
- **Formatting**: The act of creating a new file system on a storage device, preparing it for use.

### Key Structures
- **Superblock Structure**: Contains metadata about the entire file system instance.
- **Inode Structure**: Exists for every object in a file system; it indexes files and stores their attributes.
- **Dentry Structure**: Facilitates quick lookups by linking filenames to their corresponding inodes.

### Additional Functions
- **`fsync`**: A system call used to flush changes made to a file to disk, ensuring data integrity.
- **`flock`**: A function that provides advisory locking on files to prevent concurrent access issues.

### Maximum File Size
- The maximum allowable size for files in Linux is typically set at **128 TB**, depending on the specific file system being utilized.

### References to `glibc`
For detailed structures related to superblock, inode, and other filesystem components, refer to the GNU C Library (`glibc`), which provides definitions and functionalities necessary for managing these structures effectively.

Citations:
[1] https://www.baeldung.com/linux/monolithic-kernel
[2] https://learning.lpi.org/en/learning-materials/010-160/4/4.3/4.3_01/
[3] https://www.geeksforgeeks.org/monolithic-architecture/
[4] https://stackoverflow.com/questions/1806585/why-is-linux-called-a-monolithic-kernel
[5] https://www.reddit.com/r/linux/comments/1aoiaqm/the_linux_concept_journey_monolithic_kernel/
[6] https://en.wikipedia.org/wiki/Linux_kernel
[7] https://www.javatpoint.com/monolithic-structure-of-operating-system
[8] https://www.educative.io/answers/introduction-to-the-monolithic-kernel
[9] https://www.geeksforgeeks.org/monolithic-kernel-and-key-differences-from-microkernel/