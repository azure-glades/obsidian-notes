The circuits which are capable of retaining their state as long as power is applied are *static memories*
The circuits that require periodic refresh cycles to retain their state are *dynamic memories*

>[!NOTE] **Memory Latency**
>Memory latency is defined as the time it takes to transfer a single word of data to or from the memory
>- Essentially, latency measures the delay between a request for data and the actual availability of that data.
>- Faster clock cycle means lesser latency since less time is taken for transferring a word of data
>

> [!NOTE] **Memory Bandwidth**
> Memory bandwidth refers to the number of bits or bytes that can be transferred in one second.
>    - Bandwidth measures the volume of data transferred.
>    - Larger data bus increases bandwidth since more bits can be transferred per cycle.   
>   

- **High latency** can cause delays in processing, as the processor has to wait longer for data to arrive.
 - **High bandwidth** allows for the quick transfer of large amounts of data, which can improve the performance of tasks that require significant data movement.

## Static RAM
- **State Retention**: **Static RAM (SRAM)** is characterized by its ability to *retain its state as long as power is applied.* DRAM meanwhile needs *Periodic refreshing*
- SRAM cells are a type of *flip-flop circuit implemented using MOSFETs.*
    - Transistors within the cell act as switches, controlled by the word line. These transistors connect the latch to the bit lines, allowing the data to be read or written.
![[Pasted image 20250131165205.png]]

-> **Read Operation**: To read the state of an SRAM cell, the word line is activated, closing the transistors. This allows the Sense/Write circuit to detect the cell's state: if the cell is in state 1, the signal on bit line _b_ is high, and the signal on bit line _b̄_ is low. The opposite is true if the cell is in state 0. The Sense/Write circuit then sets the corresponding output.
-> **Write Operation**: During a write operation, the **Sense/Write circuit drives the bit lines** rather than sensing them. By placing the appropriate value on bit line _b_ and its complement on _b̄_, and then activating the word line, the cell is forced into the corresponding state. Once the word line is deactivated, the cell retains this new state.

### CMOS SRAM
- A common implementation of SRAM uses CMOS (Complementary Metal-Oxide-Semiconductor) technology. In a CMOS SRAM cell, transistor pairs form the inverters in the latch. For instance, in state 1, certain transistors are on to maintain the voltage at a high level, while others are off.
    - A key advantage of **CMOS SRAM** is its **very low power consumption**. *Current only flows when the cell is being accessed*; otherwise, transistors are turned off, preventing a continuous electrical path between the power supply and ground.
![[Pasted image 20250131165541.png]]

- **Typical Use Case**: Due to its speed, **SRAM** is commonly used in **cache memory**, which needs to provide fast access to frequently used data.

In summary, Static RAM (SRAM) uses latches to hold data as long as power is supplied. It has fast access times and is typically used in cache memory, but it is volatile, losing its data when power is interrupted. CMOS SRAM offers the advantage of low power consumption due to current only flowing when the cell is accessed.

## Dynamic RAM
-  A DRAM cell is implemented using a *MOS capacitor*
- State Retention and Refreshing: Unlike SRAM, DRAM does not retain its state indefinitely.
	- *The capacitor in a DRAM cell begins to discharge after the transistor is turned off, so the stored information must be periodically refreshed.* 
	- Refreshing involves restoring the capacitor charge to its full value, and this can happen when the contents of the cell are read or when new information is written into it.
![[Pasted image 20250131171011.png]]


- Because of its simpler cell structure, DRAM is more dense, meaning it has a *higher packing density* (more cells per unit area). DRAM is also less expensive than comparable SRAM. This makes DRAM suitable for use as main memory.

### Asynchronous DRAM 
- **Address Multiplexing**: To reduce the number of pins on the chip, asynchronous DRAMs use *multiplexed address inputs.* The address is divided into two parts: ***high-order bits for the row address** and **low-order bits for the column address.***
- RAS and CAS: The row address is applied first and latched using the *Row Address Strobe (RAS) signal*. Then, the column address is applied and latched using the *Column Address Strobe (CAS) signal*. A memory controller circuit is needed to achieve this multiplexing since a processor issues all address bits at the same time.
    - Example: A 256-Megabit asynchronous DRAM chip can be configured as 32M x 8, which means it has $32*1024^2$ memory locations, each storing 8 bits.
![[Pasted image 20250205191901.png]]
*Steps:*
- RAS is stored in Row address latch and selects the Row
- CAS is stored in Column address latch and selects the Column
- Selected word is received by Sense/Write circuit

> Fast Page Mode/Burst mode
> - A series of consecutive bytes can be read continuously by incrementing the CAS
> - The allows contiguous memory locations of a specific size (Like a block of memory) to be read and transferred to cache


### Synchronous DRAM (sDRAM)
- **Clock Synchronization**: Synchronous DRAMs (SDRAMs) are synchronized with a clock signal. This clock signal allows for the inclusion of  *refresh circuitry*, which includes a *refresh counter* to manage the addresses of rows that need to be refreshed.
- Each read/write cycle is engaged by a clock cycle. Hence the clock cycle determines the speed of read/write operations  (but there is a hard limit set by the response time of the transistors).
- For fast response times, the address and data connections of an sDRAM may be buffered using registers
	- The Sense/Write amplifiers act as latches, similar to asynchronous DRAMs.
![[Pasted image 20250205192236.png]]

-> **Read Operation:** All contents of a selected row are transferred to sense/write latches which are then stored on *buffer registers*. This data in the buffer is visible over the *data registers/bus*. A buffer is needed since it can only read 1 word per cycle. So to read and return a block, a buffer is needed
-> **Write Operation:** Exact same process as read operation but the information is rewritten and then stored on buffer.
- Buffer registers prevent latency when transferring/reading large blocks of data.
 
### Double-Data-Rate sDRAM (DDR sDRAM)
   - DDR sDRAM transfer data on *both the rising and falling edges of the clock*. 
    - There are many DDR chips, called DDR2, DDR3, DDR4 which have higher clock frequencies (400 and 800 MHz respc).
	    - Since there are 2 transfers per clock cycle, effective speed is 800 and 1600 MHz (i.e 800 x 10^6 read/writes per second)

-> Read write of Data from RAM is managed by the MMU
![[Pasted image 20250205192633.png]]