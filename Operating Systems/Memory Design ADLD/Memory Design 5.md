## Memory Hierarchy
![[Pasted image 20250205193055.png]]

## Cache memory
- **Locality of Reference**
	- Temporal and Spacial
- **Mapping Function**
- **Replacement Algorithm**

## Cache mapping
1. Direct mapping
2. Associative mapping
3. Set-Associative mapping

## Cache Coherence
- Ensuring the memory in cache and corresponding RAM synchronized and store the same data always
	- Any change/write done to cache is shown with *dirty bit*
	- *Valid-Invalid bit* is used for protection.
		- If Valid bit = 0, then the block of memory is not mapped
		- If valid bit = 1, then the block of memory is mapped and is in use

- Cache hit -> when memory block is in cache
	- Read hit, Write hit 
		- *write-through*: where it is directly written to RAM and cache together
		- *Write-back*: where it is written to Cache and dirty bit -> 1 (to show the RAM needs to be updated)
- Cache miss -> when memory block is not in cache and RAM is accessed
	- Read miss
		- Either the word is moved to cache and sent to processor, or it is sent to processor, then loaded to cache
	- Write miss
		- *write-through:* RAM is updated directly without bringing to cache
		- *write-back:* memory is brought to cache and then updated