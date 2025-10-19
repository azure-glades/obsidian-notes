[[Type of Data structures]]
*Definition:*
A hash table is a complex, non-linear data structure that utilizes a hash function to assign keys to different locations in a table.

A hash table uses a **hash function** to compute an index (or hash code) from a given key. This index indicates where the corresponding value is stored in an underlying array. The basic operations of a hash table include:
- **Insertion**: Adding a new key-value pair.
- **Lookup**: Retrieving the value associated with a specific key.
- **Deletion**: Removing a key-value pair from the table.
The efficiency of these operations is primarily dependent on the quality of the hash function and how well it distributes keys across the available slots in the array- Output of hash-function is always the same for a set of inputs

- **Collision**: When an element is given an index that is already filled by another element.
	- Occurs when the hash function gives the same output for different elements
	- Collisions are resolved by *probing* or *separate chaining*
- [[Probing]]: A collision resolution strategy where nearby indices are probed for empty spaces and filled with the colliding elements
	- Linear probing
	- Quadratic probing
	- Double hashing
- **Clustering:** Clustering in hash tables refers to the grouping of keys that hash to the same or nearby indices, leading to performance degradation. This causes keys to accumulate in clustered groups with empty spaces between.
	- It increases search and retrieval times and results in inefficient memory usage
	- **Primary clustering:** Occurs in linear probing when consecutive slots become filled after collisions. It increases search time since longer probing sequences are needed
	- **Secondary clustering:** Occurs in double hashing when multiple keys share the same initial hash and follow the same probing sequence. It has a better distribution than primary clustering, and is caused by an ill-defined 2nd hash function

> 3-4mk for theory
> 4mk for problems
> 2-3 mk for definitions

> Q. Construct a Hash table resolving collision using linear probing strategy for inputs: {30,20,56,75,31,90}  and hash function as h(k) = k (mod 11)

| Hash Index | Data -> |
| ---------- | ------- |
| 0          | 31      |
| 1          | 56      |
| 2          | 90      |
| 3          |         |
| 4          |         |
| 5          |         |
| 6          |         |
| 7          |         |
| 8          | 30      |
| 9          | 20      |
| 10         | 75      |
## Performance
### 1. Hash Function and Indexing
The hash function transforms a key into an index using a formula, typically represented as:
$$
\text{index} = h(\text{key})
$$
where $$h(\text{key}) = \text{key}\ \text{mod}\ n$$ where $n$ is the size of the table
This ensures that the index falls within the bounds of the array size. A well-designed hash function minimizes collisions—situations where different keys produce the same index—by evenly distributing keys across the array
### 2. Performance Characteristics
In terms of performance, hash tables offer average-case time complexities of $O(1)$ for search, insert, and delete operations. However, in worst-case scenarios—especially when many collisions occur—these operations can degrade to $O(n)$, where $n$ is the number of elements in the table
### 3. Collision Resolution
Collisions are inevitable in hash tables due to limited array size. Common methods for handling collisions include:
- **Chaining**: Storing multiple elements at the same index using a linked list or another structure.
- **Open Addressing**: Finding another open slot within the array using techniques like linear probing or quadratic probing
## [[Open Hashing]] (Separate Chaining)
- **Definition**: Open hashing, also known as separate chaining, allows multiple values to be stored in the same index of the hash table. Each index points to a linked list (or another data structure) that holds all entries that hash to that index.
- **Collision Handling**: When a collision occurs, the new entry is added to the linked list at the corresponding index. This method can handle an arbitrary number of keys per bucket.
- **Advantages**:
  - Easier to implement and manage since it does not require probing for empty slots.
  - No theoretical maximum load factor, allowing for more flexible storage.
  - Typically performs better with a high load factor and avoids clustering issues.
- **Disadvantages**:
  - Requires additional memory for pointers in linked lists.
  - Cache performance can be poorer due to non-contiguous memory allocation.
## Closed Hashing (Open Addressing)
- **Definition**: Closed hashing, or open addressing, involves storing all entries directly within the hash table array itself. When a collision occurs, the algorithm searches for another empty slot within the table.
- **Collision Handling**: Techniques such as linear probing, quadratic probing, and double hashing are used to find alternative slots for collided entries. Each slot can hold at most one key.
- **Advantages**:
  - Better memory locality and cache performance since all elements are stored contiguously.
  - No extra space is needed for linked structures.
- **Disadvantages**:
  - The size of the hash table must be at least as large as the number of keys, which can lead to wasted space if not managed properly.
  - Performance degrades as the load factor increases due to clustering, where groups of filled slots can lead to longer search times.

| Feature            | Open Hashing (Separate Chaining) | Closed Hashing (Open Addressing) |
| ------------------ | -------------------------------- | -------------------------------- |
| Storage            | Uses linked lists or chains      | Stores directly in the array     |
| Collision Handling | Multiple values per index        | One value per index              |
| Load Factor        | No theoretical maximum           | Maximum load factor of 1         |
| Memory Usage       | Extra memory for links           | More efficient memory usage      |
| Cache Performance  | Generally poorer                 | Generally better                 |
## Applications
Hash tables are widely used in various applications, including:
- **Database indexing**: Facilitating quick access to records based on unique keys.
- **Caching**: Storing frequently accessed data for rapid retrieval.
- **Implementing sets**: Allowing for efficient membership testing without storing duplicate values

-> [[Hashing 2]]