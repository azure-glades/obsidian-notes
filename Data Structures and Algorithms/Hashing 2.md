- Process of mapping a huge amount of data into smaller values with the help of a hash function
	- Such a table is a hash table
- To convert keys to the hash-value, a hash function is used.
- If $x$ is the stored data, then $h(x)$ is the hash-value where $h$ is the hash function
	- Types of hash function:
		1. Division method
		2. Multiplication method
		3. Mid-square method

- **Collision:** When a hash-function generates the same hash-value for 2 different keys.
- Avoiding collisions:
	- Open addressing/Closed hashing:
		- Linear probing
		- Quadratic probing
		- Double hashing
	- Separate Chaining/Open hashing

->Closed Hashing can only store a max 'n' keys, where n is the size of the hash table

1. **Linear Probing:** If a collision occurs at index $h(k)$, where $k$ is the key, the algorithm checks the next slot sequentially (i.e., $h(k) + 1$, $h(k) + 2$, etc.) until it finds an empty slot.
	- Disadvantage: Clusters are formed
2. **Quadratic Probing:** Using $i^2$ instead of $i$ . Works like linear hashing, instead we choose squares as next slots
3. **Double hashing:** Using 2 hash-functions. If collision happens, a 2nd hash-function is used to reassign/find new numbers
	- Ex:
		$h(x) = h_1(x) + i*h_2(x)$ where $h_1$ is the primary hashing function. $i$ varies according to possible values in $h1$ and $h_2$ is never 0

1. **Separate Chaining:** Uses a linked list to store collided keys on the same position.