**Probing** is a technique used in hash tables to resolve collisions, which occur when two keys hash to the same index. When a collision happens, probing allows the algorithm to find an alternative open slot in the hash table for the new key. There are several common types of probing methods, each with its own approach to handling collisions.
## Common Types of Probing
### 1. Linear Probing
   - **How It Works**: In linear probing, if a collision occurs at index $h(k)$, where $k$ is the key, the algorithm checks the next slot sequentially (i.e., $h(k) + 1$, $h(k) + 2$, etc.) until it finds an empty slot.
   - **Example**: If inserting key 11 at index 5 results in a collision, the algorithm will check index 6, then 7, and so on until it finds an empty slot.
   - **Advantages**: Simple to implement and provides good cache performance due to locality of reference.
   - **Disadvantages**: Can lead to clustering, where a group of consecutive filled slots can slow down search times.
### 2. Quadratic Probing
   - **How It Works**: Quadratic probing resolves collisions by checking slots at intervals that are squared. For example, if a collision occurs at index $h(k)$, it checks $h(k) + 1^2$, $h(k)+ 2^2$$h(k) + 3^2$, etc.
   - **Example**: If inserting key 11 at index 5 results in a collision, it would check index 6 (5+1^2), then index 9 (5+2^2), and so forth.
   - **Advantages**: Reduces clustering compared to linear probing by spreading out the occupied slots more evenly.
   - **Disadvantages**: Still susceptible to secondary clustering and may leave some slots unfilled.
### 3. [[Double Hashing]]
   - **How It Works**: Double hashing uses a second hash function to calculate the step size for probing. If a collision occurs at index $h_1(k)$, the next index is calculated as $h_1(k) + i \cdot h_2(k)$, where $i$ is the probe number and $h_2(k)$ is another hash function.
   - Ex: $h(x) = h_1(x) + i*h_2(x)$ where $h_1$ is the primary hashing function. $i$ varies according to possible values in $h1$ and $h_2$ is never 0
   - **Advantages**: Provides better distribution of keys and minimizes clustering issues.
   - **Disadvantages**: More complex due to the need for two hash functions.
