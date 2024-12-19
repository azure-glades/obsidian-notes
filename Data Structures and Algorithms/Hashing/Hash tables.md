[[Type of Data structures]]
- Data structure that has the fastest insertion, deletion, retrieval and searching.
- Implemented using a hash-function that stores data at specific locations calculated from the hash-function
- Output of hash-function is always the same for a set of inputs
- Collision: when different elements give the same output for a hash-function

Probing??
- Linear probing
- Quadratic probing

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


AI generated ->
## 1. Overview of Hash Tables
Hash tables are a fundamental data structure used in computer science to implement associative arrays, which store key-value pairs. They are designed to provide efficient data retrieval, insertion, and deletion operations.
### 1.1. **Definition and Functionality**
A hash table uses a **hash function** to compute an index (or hash code) from a given key. This index indicates where the corresponding value is stored in an underlying array. The basic operations of a hash table include:
- **Insertion**: Adding a new key-value pair.
- **Lookup**: Retrieving the value associated with a specific key.
- **Deletion**: Removing a key-value pair from the table.
The efficiency of these operations is primarily dependent on the quality of the hash function and how well it distributes keys across the available slots in the array[1][2][3].
### 1.2. **Hash Function and Indexing**
The hash function transforms a key into an index using a formula, typically represented as:
$$
\text{index} = h(\text{key}) \mod \text{array\_size}
$$
This ensures that the index falls within the bounds of the array size. A well-designed hash function minimizes collisions—situations where different keys produce the same index—by evenly distributing keys across the array[1][4][5].
### 1.3. **Collision Resolution**
Collisions are inevitable in hash tables due to limited array size. Common methods for handling collisions include:
- **Chaining**: Storing multiple elements at the same index using a linked list or another structure.
- **Open Addressing**: Finding another open slot within the array using techniques like linear probing or quadratic probing
### 1.4. **Performance Characteristics**
In terms of performance, hash tables offer average-case time complexities of $O(1)$ for search, insert, and delete operations. However, in worst-case scenarios—especially when many collisions occur—these operations can degrade to $O(n)$, where $n$ is the number of elements in the table
### 1.5. **Applications**
Hash tables are widely used in various applications, including:
- **Database indexing**: Facilitating quick access to records based on unique keys.
- **Caching**: Storing frequently accessed data for rapid retrieval.
- **Implementing sets**: Allowing for efficient membership testing without storing duplicate values
### 1.6. **Conclusion**
Hash tables are powerful data structures that enable fast data access through effective key-value mapping. Their design and implementation play crucial roles in optimizing performance across diverse computing applications.

## 2. Open Hashing (Separate Chaining)
- **Definition**: Open hashing, also known as separate chaining, allows multiple values to be stored in the same index of the hash table. Each index points to a linked list (or another data structure) that holds all entries that hash to that index.
- **Collision Handling**: When a collision occurs, the new entry is added to the linked list at the corresponding index. This method can handle an arbitrary number of keys per bucket.
- **Advantages**:
  - Easier to implement and manage since it does not require probing for empty slots.
  - No theoretical maximum load factor, allowing for more flexible storage.
  - Typically performs better with a high load factor and avoids clustering issues.
- **Disadvantages**:
  - Requires additional memory for pointers in linked lists.
  - Cache performance can be poorer due to non-contiguous memory allocation.

## 3. Closed Hashing (Open Addressing)
- **Definition**: Closed hashing, or open addressing, involves storing all entries directly within the hash table array itself. When a collision occurs, the algorithm searches for another empty slot within the table.
- **Collision Handling**: Techniques such as linear probing, quadratic probing, and double hashing are used to find alternative slots for collided entries. Each slot can hold at most one key.
- **Advantages**:
  - Better memory locality and cache performance since all elements are stored contiguously.
  - No extra space is needed for linked structures.
- **Disadvantages**:
  - The size of the hash table must be at least as large as the number of keys, which can lead to wasted space if not managed properly.
  - Performance degrades as the load factor increases due to clustering, where groups of filled slots can lead to longer search times.

| Feature               | Open Hashing (Separate Chaining) | Closed Hashing (Open Addressing) |
|-----------------------|-----------------------------------|-----------------------------------|
| Storage               | Uses linked lists or chains       | Stores directly in the array      |
| Collision Handling     | Multiple values per index         | One value per index               |
| Load Factor           | No theoretical maximum            | Maximum load factor of 1          |
| Memory Usage          | Extra memory for links            | More efficient memory usage       |
| Cache Performance     | Generally poorer                  | Generally better                  |

## 4. Probing in Hash Tables
**Probing** is a technique used in hash tables to resolve collisions, which occur when two keys hash to the same index. When a collision happens, probing allows the algorithm to find an alternative open slot in the hash table for the new key. There are several common types of probing methods, each with its own approach to handling collisions.

### 4.1. Common Types of Probing
1. **Linear Probing**
   - **How It Works**: In linear probing, if a collision occurs at index $h(k)$, where $k$ is the key, the algorithm checks the next slot sequentially (i.e., $h(k) + 1$, $h(k) + 2$, etc.) until it finds an empty slot.
   - **Example**: If inserting key 11 at index 5 results in a collision, the algorithm will check index 6, then 7, and so on until it finds an empty slot.
   - **Advantages**: Simple to implement and provides good cache performance due to locality of reference.
   - **Disadvantages**: Can lead to clustering, where a group of consecutive filled slots can slow down search times.

2. **Quadratic Probing**
   - **How It Works**: Quadratic probing resolves collisions by checking slots at intervals that are squared. For example, if a collision occurs at index $h(k)$, it checks $h(k) + 1^2$, $h(k)+ 2^2$$h(k) + 3^2$, etc.
   - **Example**: If inserting key 11 at index 5 results in a collision, it would check index 6 (5+1^2), then index 9 (5+2^2), and so forth.
   - **Advantages**: Reduces clustering compared to linear probing by spreading out the occupied slots more evenly.
   - **Disadvantages**: Still susceptible to secondary clustering and may leave some slots unfilled.

3. **Double Hashing**
   - **How It Works**: Double hashing uses a second hash function to calculate the step size for probing. If a collision occurs at index $h_1(k)$, the next index is calculated as $h_1(k) + i \cdot h_2(k)$, where $i$ is the probe number and $h_2(k)$ is another hash function.
   - **Example**: If inserting key 11 results in a collision at index 5, and using a secondary hash function gives a step size of 3, the next indices checked would be 8 (5+3), then 11 (8+3).
   - **Advantages**: Provides better distribution of keys and minimizes clustering issues.
   - **Disadvantages**: More complex due to the need for two hash functions.

### 4.2. Summary
Probing is essential for maintaining efficient operations in hash tables when collisions occur. The choice of probing technique can significantly impact performance:
- **Linear Probing** is straightforward but may lead to clustering.
- **Quadratic Probing** mitigates some clustering issues but can still suffer from secondary clustering.
- **Double Hashing** offers improved distribution but requires more complex calculations.
Understanding these methods helps in selecting the appropriate collision resolution strategy based on specific application requirements and expected data patterns.
