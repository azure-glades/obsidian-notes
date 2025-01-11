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
