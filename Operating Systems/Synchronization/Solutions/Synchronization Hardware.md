Solutions for the critical section problem that is implemented through hardware, and not software
- Needed because software solutions need not work on all computer architectures

Consider an example problem where 2 threads are accessing a shared variable `x = 0` and starts with `bool flag = false`
```thread 1
while(flag != true)
	//busy looping;
print x;
```
```thread 2
x = 100;
flag = true;
```

While the expected outcome is `x : 100`, processor re-ordering can cause `x : 0` where `flag = true` is run before `x = 100`. Similarly, `print x` can also be run before entering the `while loop`  putting out  `x : 0`
	This is irrational behaviour which causes bugs in code
## 1. Memory Barriers
Manner in which OS provides memory access to processes is called a memory model
- **Strongly Ordered:** Memory modification in a processor is immediately visible to all others.
- **Weakly Ordered**: Memory modification in a processor may not be visible immediately
Since not all memory models support this, computer architectures provide instructions that can *force* any change in memory to be propagated across all processors to ensure up-to-date memory access.
-> These are *memory barriers* or *memory fences*.

Example: 2 Threads simultaneously accessing a shared variable x
```thread 1
while(!flag)
	memory_barrier();
print x;
```
```thread 2
x = 100;
memory_barrier();
flag = true;
```
 The `memory_barrier()` prevents re-ordering of operations and ensures they are run in sequence. Also updates the value of x to all the processors.
 > Memory barriers are considered low-level operations only used when writing kernel modules

## 2. Hardware Instructions
Special hardware instructions/functions that are used in modifying and manipulating memory addresses  *atomically*, via
- `test_and_set()` instructions
- `compare_and_swap()` instructions

### 2.1. Test-and-Set (TAS)
Implements a function that tests if a `lock` value is true or false, and then sets the value to true.
- If `lock = false`:
	- `rv` = `false` -> busy-wait loop is exited
	- set `lock` = true before exiting loop
	- run critical section
- if `lock = true`:
	- `rv` = `true` -> busy-wait loop is not exited
	- `lock` remains = true.
	- busy waiting until another processes sets `lock = false`
```c
bool test_and_set(boolean *target) {
	bool rv = *target;
	*target = true;
	return rv;
}

main(){
	do{
		while(test_and_set(&lock)) {
			/*busy wait as long as lock = true*/
		}
		// Lock was false, and hence while loop exited
		// Set lock = true before exiting while loop
		
		/*critical section */
		lock = false;
		
		/*remainder section */
	} while (true) //always check for sharing
}
```
- If two `test_and_set()` functions are executed on different processors, the functions execute sequentially, but in arbitrary order

### 2.2. Compare-and-Swap (CAS)
Implements a function that compare two possible values and transfer control based on current value of lock.
CAS implements bounded-waiting
- if `lock = 0`:
	- returns `key = 0` -> exits the busy-wait loop
	- inform that the process is no longer waiting and has control
	- run critical section
- if `lock = 1`:
	- returns `key = 1` -> stays busy-waiting
	- `lock` remains `1` , being used by another process
	- busy waiting until another process sets `waiting = false` and gives it access
```c
int compare_and_swap(int *value, int expected, int new value) {
	int temp = *value;
	if (*value == expected)
		*value = new value;
	return temp;
}

while (true) {
	waiting[i] = true; //informs process i wants to enter critical section
	key = 1; //indicates the lock is not acquired yet
	
	while (waiting[i] && key == 1) //busy waiting to acquire lock
		key = compare and swap(&lock,0,1);
	
	waiting[i] = false; //process i has got control of lock
	//does not need to inform that it is waiting, hence set to false
	
	/* critical section */
	
	j = (i + 1) % n; // n is number of processes present
	while ((j != i) && !waiting[j]) //checking if other process needs access
		j = (j + 1) % n;
	if (j == i) //if no other process needs access
		lock = 0;
		/* frees up the lock to allow
		any subsequent process to run critical section */
	else
		waiting[j] = false; 
		//transferring control to other process by exiting its busy-wait loop
	
	/* remainder section */
}

```

## 3. Atomic Variables
Basic data types can be defined as atomic variables, which causes any modification/manipulation functions to run atomically.
- Often implemented as a special atomic data type, using CAS operations
Example: `increment(&sync)` on an atomic data type `sync`
```c
void increment(atomic_t *v)
{
	int temp;
	do {
		temp = *v;
	} while (temp != compare_and_swap(v, temp, temp+1));
}
```
