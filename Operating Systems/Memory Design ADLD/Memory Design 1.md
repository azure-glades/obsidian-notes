- available memory chip = `N x W` where N is no of words, W is Word size.
- required memory size: `N' x W'`
We need `p x q` amount of chips, where `p = N'/N` and `q = M'/M`
Horizontal expansion -> increasing the word size
Vertical expansion -> increasing the number of words
Matrix expansion -> both
> Ex: Vertical expansion
> 1. We have (128, 8) RAM chip. We need (512, 8) RAM chip.
> Hence, p = 512/128 = 4. q = 8/8 = 1. We need 4 RAM chips
> 2. Address bits , 512 = $2^9$ . Hence each memory address is 9 bits long. There are $2^9 * 8$ bits of memory
>  3. Since we use 4 chips, we use a 2:4 decoder
>  4. Draw decoder connected to 4 RAM chips diagram
>  Since it is 2:4 decoder, decoder uses 2 bits to reference the chip. So the first 2 bits of memory address is used by the decoder. The remaining 7 bits are used in the address-line of a chip (draw diagram and see) (since each chip is 128, its address is also 7 bits long, which adds up nicely)

> Ex: Horizontal expansion
> We have 1024 x 4 ram chip. We need 1024 x 8 memory. 
> Vertical expansion since word size has increased from 4 to 8

> Ex: 128 x 8 with 128 x 1 chips
> No of chips p = 128/128. q = 8/1 = 8 chips
> Decoder = No decoder (since p = 1)
> Memory address has 7 bits (because 128 = 2^7)

(AI GENERATED ->)
**I. Introduction to Memory Systems**

- **Basic Concepts**:
    - Maximum memory size is determined by the addressing scheme.
    - Address space is the range of memory locations a computer can access.
    - Address, data, and control lines connect the processor and memory.
    - **MAR (Memory Address Register)** and **MDR (Memory Data Register)** facilitate data transfer.
    - The size of MAR determines the addressable memory locations, and MDR determines the amount of data transferred.
    - Key design goal: Large and fast memory within cost limits.
- Techniques to improve memory:
    - **Cache memory** for speed.
    - **Virtual memory** for size.

**II. Types of Memory** * Main Memory: * **Semiconductor memory**. * **RAM (Random Access Memory)**: Volatile. * **SRAM (Static RAM)**. * **DRAM (Dynamic RAM)**. * **ROM (Read Only Memory)**: Non-volatile. * Measures of Memory Speed: * **Memory Access Time**: Time between operation initiation and completion. * **Memory Cycle Time**: Minimum time between two independent memory operations. * Memory cycle time is slightly larger than memory access time.

**III. Memory Cell Organization** * Memory cells are organized in an array. * Each cell stores one bit. * Rows are connected to word lines; columns to Sense/Write circuits. * **Read operation**: Sense/Write circuits read data from selected cells. * **Write operation**: Sense/Write circuits store data in selected cells. * Example of memory circuit with 16 words of 8 bits each (16 x 8 organization). * Larger memory circuits (e.g., 1K memory) require more external connections. * Address bits can be divided to form row and column addresses.

**IV. Static RAM (SRAM)** * **Static RAM (SRAM)**: Retains state as long as power is applied. * Implemented with cross-connected inverters forming a latch. * Transistors act as switches controlled by the word line. * **Read Operation**: Word line activates transistors to sense the cell's state. * **Write Operation**: Sense/Write circuit drives bit lines to force the cell into a state. * **CMOS SRAM**: Low power consumption; current flows only during access. * **Volatile memory**: Contents lost when power is interrupted. * Fast access times (few nanoseconds). * Used where speed is critical (e.g., cache memory).

**V. Dynamic RAM (DRAM)** * **Dynamic RAM (DRAM)**: Simpler and smaller cells than SRAM. * Uses a capacitor and transistor. * Does not retain state indefinitely, requires periodic refreshing. * **Refresh**: Contents are refreshed when read or written. * More dense and less expensive than SRAM. * **Asynchronous DRAM**: * Row and column addresses are multiplexed to reduce pins. * **RAS (Row Address Strobe)** and **CAS (Column Address Strobe)** control address loading. * Example: 256-Megabit chip (32M x 8). * **Synchronous DRAM (SDRAM)**: * Synchronized with a clock signal. * Built-in refresh circuitry. * Buffered address and data connections. * Various modes of operation. * **Double-Data-Rate SDRAM (DDR SDRAM)**: * Transfers data on both rising and falling edges of the clock. * Faster versions: DDR2, DDR3, DDR4.

**VI. Latency and Bandwidth** * **Memory Latency**: Time to transfer a word to or from memory. * **Memory Bandwidth**: Number of bits/bytes transferred per second. * Bandwidth is determined by transfer rate and data bus width.

**VII. Read-Only Memory (ROM)** * **Non-Volatile memory**: Retains contents after power is off. * **ROM**: Data written during manufacturing. * **PROM (Programmable ROM)**: Data loaded by user, irreversible process. * **EPROM (Erasable PROM)**: Can be erased and reprogrammed, uses UV light. * **EEPROM (Electrically Erasable PROM)**: Can be erased electrically. * **Flash Memory**: Similar to EEPROM, higher density, low power consumption, uses blocks.

%% VIII. Memory Controller * Handles multiplexed address inputs for dynamic memory. * Inserts between the processor and the memory. %%

**IX. Cache Memory** * **Cache memory** makes main memory appear faster to the processor. * Based on "locality of reference" in programs. * **Temporal locality**: Recently executed instructions are likely to be executed again soon. * Cache stores a subset of main memory blocks. * **Mapping Function**: Determines which main memory blocks reside in the cache. * **Replacement Algorithm**: Chooses which block to replace when the cache is full.

**X. Cache Mapping Techniques** * **Direct Mapping**: Each main memory block maps to a specific cache block. * Simple but can lead to contention. * Address fields: Word, Block, Tag. * **Associative Mapping**: Main memory block can be placed in any cache block. * More flexible, efficient use of cache space. * More complex due to tag searching. * Address fields: Word, Tag. * **Set Associative Mapping**: Blocks are grouped into sets. * A compromise between direct and associative mapping. * Address fields: Word, Set, Tag.

**XI. Cache Operations** * Processor interacts with cache transparently. * **Cache Hit**: Data is found in the cache. * **Read hit**: Data is obtained from the cache. * **Write hit**: Cache and main memory updated. * **Write-through protocol**: Updates both cache and main memory simultaneously. * **Write-back protocol**: Updates only the cache, main memory updated on replacement. * **Cache Miss**: Data not in cache. * **Read miss**: Block is transferred from main memory to cache. * **Write miss**: Depends on the protocol. * **Write-through**: Main memory updated directly. * **Write-back**: Block brought into cache, then updated.

**XII. Cache Coherence** * **Valid bit**: Indicates if a block contains valid data. * Data transfers between main memory and disk bypass the cache. * **Cache coherence problem**: Inconsistent data copies between cache and main memory. * Can happen with write-back protocol when disk and main memory are changed. * Possible solution: Force a write-back before main memory is updated from the disk.

**XIII. Examples and Calculations** * Examples of address mapping in caches. * Cache address format calculations for direct and set associative caches. * Calculations of effective access time. * Calculations of speed up using on chip cache. * Calculations of MAR, MBR sizes and number of chips needed for a design. * Design a 16K-by-8 memory using 2K-by-4 memory chips and decoding circuitry.

This outline covers the main concepts and should be a good basis for your study notes. Let me know if you'd like me to elaborate on any specific topic or calculation or if you would like to explore some aspects of the material in more detail.