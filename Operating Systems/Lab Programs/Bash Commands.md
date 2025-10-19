## 1. cp
```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <errno.h>
#include <sys/types.h>
#include <unistd.h>

#define BUFFER_SIZE 8192

int main(int argc, char* argv[])
{
	int input_fd, output_fd;
	//input and output file descriptors
	ssize_t byte_in, byte_out; //Number of bytes returned by read() and write()
	char buffer[BUFFER_SIZE];

	if(argc != 3)
	{
		printf("Usage: cp file1 file2\n"); //if file arguments are missing
		return 1;
	}
	//creating input file descriptor
	input_fd = open(argv[1], O_RDONLY);
	if(input_fd == -1)
	{
		perror("open");
		return 2;
	}
	
	//creating output file descriptor
	output_fd = open(argv[2], O_WRONLY | O_CREAT, 0644);
	if(output_fd == -1)
	{
		perror("open");
		return 3;
	}

	//copy process
	while((byte_in = read(input_fd, &buffer, BUFFER_SIZE))>0)
	{
		byte_out = write(output_fd, &buffer, (ssize_t)byte_in);
		if(byte_out != byte_in)
		{
			perror("write");
			return 4;
		}
	}
	
	//close files
	close(input_fd);
	close(output_fd);

	return (EXIT_SUCCESS);	
}
```

## 2. [[ls]]
```c
#include <stdio.h>
#include <dirent.h>
#include <sys/stat.h>
#include <pwd.h>
#include <grp.h>
#include <time.h>

int main() {
    DIR *d;
    struct dirent *de;
    struct stat buf;
    char P[10] = "rwxrwxrwx", AP[10] = "----------"; // Initialize AP to represent no permissions
    int i;
    unsigned int j; // Declare j as unsigned int
    struct passwd *p;
    struct group *g; // Fixed the declaration of struct group
    struct tm *t;
    char time_buf[26]; // Renamed to avoid conflict with time function

    d = opendir(".");
    if (d == NULL) {
        perror("opendir");
        return 1; // Return error if the directory cannot be opened
    }

    // Read the first two entries (which we want to skip)
    readdir(d);
    readdir(d);

    while ((de = readdir(d)) != NULL) {
        if (stat(de->d_name, &buf) == -1) {
            perror("stat");
            continue; // Skip to the next file if stat fails
        }

        // File Type
        if (S_ISDIR(buf.st_mode))
            printf("d");
        else if (S_ISREG(buf.st_mode))
            printf("-");
        else if (S_ISCHR(buf.st_mode))
            printf("c");
        else if (S_ISBLK(buf.st_mode))
            printf("b");
        else if (S_ISLNK(buf.st_mode))
            printf("l");
        else if (S_ISFIFO(buf.st_mode)) // Fixed S_ISPIFO to S_ISFIFO
            printf("p");
        else if (S_ISSOCK(buf.st_mode))
            printf("s");

        // File Permissions
        for (i = 0, j = (1 << 8); i < 9; i++, j >>= 1) {
            AP[i] = (buf.st_mode & j) ? P[i] : '-';
        }
        AP[9] = '\0'; // Null-terminate the permissions string
        printf("%s", AP); // Corrected syntax

        // No. of Hard Links
        printf("%5lu", (unsigned long)buf.st_nlink); // Use %lu for unsigned long

        // User Name
        p = getpwuid(buf.st_uid);
        printf(" %.8s", p ? p->pw_name : "unknown"); // Handle NULL case

        // Group Name
        g = getgrgid(buf.st_gid); 
        printf(" %-8.8s", g ? g->gr_name : "unknown"); // Handle NULL case

        // File Size
        printf(" %8lld", (long long)buf.st_size); // Use %lld for larger files

        // Date and Time of modification
        t = localtime(&buf.st_mtime);
        strftime(time_buf, sizeof(time_buf), "%b %d %H:%M", t);
        printf(" %s", time_buf);
    
        // File Name
        printf(" %s\n", de->d_name);
    }

    closedir(d); // Don't forget to close the directory
    return 0; // Indicate successful execution
}
```

## 3. mv
```c
#include <stdio.h>
#include <dirent.h>
#include <sys/stat.h>
#include <pwd.h>
#include <grp.h>
#include <time.h>

int main(int argc, char* argv[])
{
	int infd, outfd;

	if(argc != 3)
	{
		printf("Usage: mv file1 file2");
		return 1;
	}

	infd = link(argv[1], argv[2]);
	if(infd == -1)
	{
		perror("Link error");
		return 2;
	}

	outfd = unlink(argv[1]);
	if(outfd == -1)
	{
		perror("Unlink error");
		return 3;
	}

}
```

## 4. rm
```c
#include <stdio.h>
#include <dirent.h>
#include <sys/stat.h>
#include <pwd.h>
#include <grp.h>
#include <time.h>

int main(int argc, char* argv[])
{
	int infd, outfd;

	if(argc != 3)
	{
		printf("Usage: mv file1 file2");
		return 1;
	}

	infd = link(argv[1], argv[2]);
	if(infd == -1)
	{
		perror("Link error");
		return 2;
	}

	outfd = unlink(argv[1]);
	if(outfd == -1)
	{
		perror("Unlink error");
		return 3;
	}

}
```
