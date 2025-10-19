***The Virtual File System is a Kernel software layer that handles all system calls and works as a common interface to several kinds of file systems***
- This allows a uniform API for the VFS which then handles its implementation for various different filesystems
- To access a file system, it has to be *mounted* to the linux file system. The location where the root of the filesystem joins is called the *mount point*. Usually on `/mnt`

## Types of File Systems
A file system is a system that organizes, stores, and retrieves files on a storage device.  It manages how data is stored and accessed, acting as an interface between the operating system and the physical storage. The type of file system depends largely on the storage hardware 
### Disk Based File systems
Manages memory on disks or devices that emulate disks.
- `Ext2` and `Ext3` (Extended Filesystem) are used by Linux
- `sysv` and `UFS`
- Microsoft file systems like `MS-DOS`, `VFAT` and `NTFS` (meant for the .NET kernel)
- Universal Disk Format (`UDF`), `ISO9660 CD-ROM` for DVDs and CDs

### Network File systems
Manages and accesses memory across multiple networked computers.
- `NFS`, `Coda`, `CIFS` (common internet filesystem) etc.

### Special File systems
Special file systems expose operating system elements as files, enabling interaction through the file system API.
- `/proc`
- `/swap`
- `/sudo`
- `/sys`

## Common File Model
Linux represents all the different file systems in a single common manner. This is the *common file model* where file systems may have different physical organization, which is translated into the common file model.
- This common file model is the UNIX filesystem -> The native filesystem on linux
	- Since the common file model is the UNIX filesystem, all system calls/operations within the UNIX filesystem happen with highest efficiency since no translation needs to be done 
- All filesystems, including NTFS, FAT, etc are represented/described as-per the UNIX filesystem
	- The differences between different file-systems have to be translated/handled correctly to map the system calls of VFS to the physical organization
	- Ex: To read data from NTFS, the native system-call is `ReadFile()`
		- When we try to read a file in NTFS, we call the VFS system call `read()` on the specific `file` object. This file object stores pointers to relevant NTFS syscalls. When `read()` is called, the `file` objects redirects it `op_file` parameter (which is a `struct` in C). This `op_file` stores the relevant NTFS syscalls, i.e `ReadFile()`.
			- Call: `read()` -> `file` object -> `op_file`-> `ReadFile()`. This translation is done by the Kernel.
		- Usually, if the file was in `Ext4` the `read()` syscall would invoke the kernel to read information from the file. The `op_file` would just store `read()` and translation would not be needed.

There are multiple such file system `objects` which contain structures pointing to relevant drives/syscalls. These objects are stored as Data structures.

## VFS Data Structures
The VFS object attributes are stored as structures since the entirety of Linux is written on C and hence OOP is not an option.

### Superblock
Stores metadata about the file-system, like type, size, mount-point.
- For disk-based file system, `superblock` identifies the file system control block, i.e the driver responsible for read-writing onto the disk
- `super_block` structure, checked with `IS_BLK`
Some superblock fields:
- `s_dev` - Device identifier
- `s_blocksize` - Block sizes of the file-system (in bytes)
- `s_dirt` - Dirty bit (modified bit)
- `s_type` - Filesystem type
- `s_flags` - Mount flags
- `s_magic` - Magic number of the file system
- `s_root` - directory entry (dentry) of the root of file system

- `s_unmount`, `s_lock` - semaphore used to unmount, and lock the file system

- `s_inodes` - list of inodes in file system
- `s_dirty` - list of inodes with modified dirty bits
- `s_files` - list of file objects

All superblock objects are linked in a circular doubly linked list.

### Inode (Index Node)
Indexes information about a file. Each file has an *inode number* which is unique for every file
### File
Stores information about an open file and the process accessing that file
### Dentry (Directory Entry)
Stores information about the directory entry of the file (i.e the file name and path in the file system)
![[Pasted image 20250212193132.png]]

> [!note] Dentry Cache

## File system Handling
To access file-systems, they need to be first attached to the main file system.
- The location where the root of the file-system is attached to the main file-system is called the *mount point*
- The attached file system is the child, while the main file system is the parent.
Ex:
- `/proc` file system is a child of the `root` file system. It is mounted at `/`
- Most externally attached drives are mounted at `/mnt/drive-name`
### Namespaces
The set of files that a process can access with it's permissions is called a *namespace*. It's the tree of mounted file-systems.
- Most processes *share* the same namespace and changes get updated among them, especially if the processes were made using `init()`
- If the process has been created with `clone()` with `CLONE_NEWNS` (Clone new namespace flag) it gets a new namespace.
- When a process mounts/unmounts a FS, it only modifies its namespace which is visibile to all processes sharing it.

Namespace is a structure with the following parameters:
- `count` - Atomic variable that shows how many processes share the namespace
- `root` - file-system descriptor for root of namespace
- `list` - lists all mounted file-system descriptors
- `sem` - read-write semaphore for making changes to the namespace
### Mounting
- It is possible to mount a file-system multiple times, which allows us the access the FS from multiple locations.
	- But the FS is not copied and a single `superblock` stores data regarding the FS and all its mount-points
- Locations in a mounted FS can be used as mount points for more FS.
- Multiple FS can be stacked at a single mount-point. This follows a LIFO order where the latest mounted FS is accessed. To access older FSs, the current one has to be unmounted
Information on mounted FSs is stored in a structure `vfsmount` which is a mounted file system descriptor
## Path-name Lookup
Process require `file` objects which are located by corresponding `inode` objects. The `inode` of a corresponding file is located with the *path-name*
- If it starts with `/` it is an absolute path, else it is *relative* - navigated by the current directory
Ex: `/home/hegde/documents/newfile.txt`
- `home` is the `dentry` and the `inode` with name `hegde` is searched. `hegde` has to be a `dentry`. This process is performed recursively until the last segment is reached which cannot be a `dentry`. The `inode` of that object is then passed to system calls
- This process is the traversal of a path-name, i.e path-name lookup
- The dentry cache speeds up the process since recently accessed locations are often stored in the cache.

Not all path-names can be viewed by processes. Access rights, symbolic links etc. have to be handled by the kernel.
- Accessing a directory when the process does not have read permissions terminates does not yield the inode.
- If the filename ends in a symbolic link, the traversal continues through the symbolic link.
	- Symbolic links may cause circular references which need to be handled as errors
- If the filename enters another file-system, relevant system calls need to be translated on the fly.

Path-name lookup is done with `path_lookup()` function.
Parameters:
- `name` - Pointer to the file path-name
- `flags` - Mode of access (like Read-only, write-only, read-write)
- `nd` - Address to `nameidata` struct which stores the result of the lookup operation
Returns the `nameidata` structure

> [!NOTE]+ `nameidata`
> `dentry` -> Address of the dentry object, `mnt` -> Mount point of file-system
> `last` -> last component of path name
> `flags` -> lookup flags
> There are a lot more. *See Further: Understanding the Linux Kernel, pg 496*

### Standard Path Lookup
Standard pathname lookup in Linux (without `LOOKUP_PARENT`) involves traversing a path string component by component. Here's a breakdown:
1. *Initialization & Leading Slash Removal:* The process starts by initializing flags and removing any leading slashes. An empty path at this stage returns success.

2. *Component-wise Traversal:* The path is parsed into components separated by slashes. For each component:
    - Permissions Check: The "execute" permission is checked on the current directory. Failure results in an error.
    - Hash Calculation: A hash of the component name is computed for efficient dentry cache lookup.
    - Special Cases ("." and ".."): "." (current directory) is skipped. ".." (parent directory) involves climbing up the directory hierarchy, handling mount points and root directories carefully. `follow_mount()` is crucial for navigating across filesystem boundaries.
    - Dentry Cache Lookup: `do_lookup()` is used to find the dentry for the component. It first checks the dentry cache (`__d_lookup()`). If a miss occurs, `real_lookup()` is called to read the directory from disk, create the dentry and inode, and populate the caches.
    - Symbolic Link Handling: If the component is a symbolic link, the link is resolved (described elsewhere).
    - Directory Check: For intermediate components, it's verified they are directories.

3. *Last Component Handling:* After processing all but the last component:
    - Trailing Slash Handling: A trailing slash indicates the last component should be a directory.
    - Special Cases ("." and ".."): Similar handling as in the component loop.
    - Dentry Cache Lookup: `do_lookup()` is used again for the final component.
    - Symbolic Link Handling: Symbolic links are handled if `LOOKUP_FOLLOW` is set.
    - Mount Point Check: `follow_mount()` is called to check for mount points.
    - Final Checks: Checks for a valid inode and if `LOOKUP_DIRECTORY` is set, ensures the final component is a directory.

4. *Result:* The process returns success (0) if the path is valid. The `nameidata` structure (`nd`) is updated to point to the dentry and mount of the resolved path. Errors like `ENOENT` (file not found) or `ENOTDIR` (not a directory) can be returned. The dentry cache plays a vital role in speeding up lookups.

### Parent Path Lookup
Parent pathname lookup, indicated by the `LOOKUP_PARENT` flag, focuses on resolving the _directory containing_ the last component of a path, rather than the last component itself. This is crucial for operations like file creation or deletion.
1. *Purpose:* The primary goal is to identify the parent directory of the target file or directory. This is distinct from standard lookup which resolves the entire path.

2. *`nameidata` Fields*: `LOOKUP_PARENT` sets up specific fields in the `nameidata` structure:
    - `last`: Stores the name of the final path component.
    - `last_type`: Indicates the type of the last component (e.g., `LAST_NORM` for regular filename, `LAST_ROOT` for "/", `LAST_DOT` for ".", `LAST_DOTDOT` for "..", `LAST_BIND` for a symbolic link into a special filesystem). `LAST_ROOT` is the initial default.

3. *Process:* The lookup process mirrors standard lookup up to a point:
    - Initial Steps: Similar initialization and leading slash removal as in standard lookup.
    - Component Traversal: The path is traversed component by component, performing permission checks, hash calculations, handling "." and "..", and looking up dentries in the cache, just like in standard lookup.
    - Up to Step 8 (Standard Lookup): The process is identical to standard lookup until step 8.

4. *Divergence from Standard Lookup (from Step 8):* Here's where parent lookup differs:
    - Last Component Handling: _Instead of resolving the last component_, the process focuses on identifying its type and storing its name.
    - Type Classification: `nd->last_type` is set based on the last component's name: `LAST_DOT`, `LAST_DOTDOT`, or defaults to `LAST_NORM`.
    - No Resolution: The last component itself is _not_ resolved. `do_lookup()` is not called for the last component.

5. *Result*: The function returns 0 (success). Critically, the `dentry` and `mnt` fields of the `nameidata` structure point to the _parent directory_ of the last component, not the last component itself. This is the key difference between standard and parent lookups. The `last` and `last_type` fields provide information about the final component without actually resolving it.

### Symbolic Lookup
Symbolic link lookup handles pathnames containing symbolic links, which are files storing paths to other files. The kernel must resolve these links during pathname traversal. The process is recursive but carefully controlled to prevent infinite loops.
1. *Symbolic Link Identification:* During standard pathname lookup (`link_path_walk()`), when a component's inode has a `follow_link` method, it's identified as a symbolic link.

2. *`do_follow_link()`*: This function manages the symbolic link resolution:
    
    - Loop Prevention: Checks `current->link_count` (nested link depth, max 5) and `current->total_link_count` (total links followed, max 40) to prevent loops and excessive processing. Returns `-ELOOP` if limits are exceeded.
    - Rescheduling: Calls `cond_resched()` to allow other processes to run if needed.
    - Counters & Depth: Increments `current->link_count`, `current->total_link_count`, and `nd->depth` to track link resolution.
    - `follow_link` Method: Calls the filesystem-specific `follow_link` method of the symbolic link's inode. This method extracts the target pathname stored within the link and saves it in the `nd->saved_names` array.
    - `__vfs_follow_link()`: Invokes this function to further process the extracted pathname.
    - `put_link` Method: If defined, calls the `put_link` method to release any resources used by the `follow_link` method.
    - Decrement Counters: Decrements `current->link_count` and `nd->depth`.
    - Return: Returns the result of `__vfs_follow_link()`.
3. *`__vfs_follow_link()`*: This function handles the actual resolution of the symbolic link's target path:

    - Absolute Path Check: Checks if the symbolic link's target path is absolute (starts with a `/`). If so, it releases any prior path information and resets the `nameidata` structure to the root directory.
    - Recursive `link_path_walk()`: Recursively calls `link_path_walk()` with the symbolic link's target path. This handles cases where the target path itself contains further symbolic links.
    - Return: Returns the result of the recursive `link_path_walk()` call.
4. *Resumption*: After `do_follow_link()` completes, the original `link_path_walk()` resumes its traversal from the resolved target of the symbolic link.

5. *Nesting and Limits:* The recursive nature of the process allows for nested symbolic links, but the link counters and depth limit prevent infinite recursion and denial-of-service attacks.

## VFS System Calls
The key characteristic of a VFS  system call is that it's _abstracted_. Instead of being specific to a particular file system type (like ext4, XFS, or NFS), the call uses a generic interface.
- The VFS layer then translates these generic calls into the appropriate operations for the actual file system in use
- This abstraction is what enables Linux (and other operating systems with a VFS) to support a wide variety of file systems seamlessly

### `open()` 
### `read()` and `write()`
### `close()`


## File Locking
Linux supports all types of file locking, including *advisory locks* and *mandatory locks*.
Implements the `fcntl()` and `flock()` system calls
A process can acquire or release an advisory file lock in two ways:
- **`flock()` System Call:** Takes the file descriptor (`fd`) and a command specifying the lock operation as arguments. `flock()` locks the _entire_ file.
- **`fcntl()` System Call:** Takes the file descriptor (`fd`), a command specifying the lock operation, and a pointer to a `flock` structure as arguments. The `flock` structure allows specifying the portion of the file to be locked. This enables a process to hold multiple locks on different parts of the same file.