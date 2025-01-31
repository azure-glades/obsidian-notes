
## Introduction
- **Maximum Memory Size and Addressing Scheme**: The *addressing scheme* of a computer dictates the maximum memory size it can utilize. For instance, a 16-bit address can access 2^16 = 64Kb memory locations, a 32-bit address can access 2^32 = 4Gb locations, and a 64-bit address can access 2^64 = 16 Exabyte locations. The number of locations that can possibly be addressed is the *addressable memory space.*
	- **Address Space**: The total range of memory locations that a computer can address. It's essentially the size of the memory that the processor can access using its addressing scheme.

- **Processor-Memory Connection**: The connection between a processor and its memory is established through three sets of lines: *address lines, data lines, and control lines.*
    - **Address lines** are used by the processor to specify the particular memory location involved in a data transfer.
    - **Data lines** are used to transfer the actual data between the processor and the memory.
    - **Control lines** carry commands indicating whether a **Read** or **Write** operation is required, the size of the data transfer (e.g., byte or word), and timing information.
- **Memory Address Register (MAR) and Memory Data Register (MDR)**: Data transfer between the main memory and the CPU happens through two CPU registers, the MAR and the MDR.
    - The **MAR** holds the address of the memory location that is being accessed. If the MAR is _k_-bits, then the total addressable memory location is 2^k.
    - The **MDR** holds the data that is being transferred to or from the memory. If the MDR is _n_-bits, then _n_ bits of data are transferred in one memory cycle -> Its the width of the bus.
    - These registers work in tandem with control lines, such as **Read**, **Write**, and **Memory Function Complete (MFC)**, to coordinate data transfer.

- **Key Design Goal**: A crucial goal in computer system design is to provide as large and as fast a memory as possible while staying within a given cost target.
- **Techniques to improve memory**:
    - **Cache memory** is used to increase the effective speed of memory access. It acts as a fast buffer between the processor and main memory.
    - **Virtual memory** is used to increase the effective size of memory, allowing programs to use more memory than physically available.

> The addressing scheme and the size of the MAR determine the total accessible memory, while the data transfer between processor and memory is managed by data, address, and control lines using the MAR and MDR. The main goal is to provide large fast and efficient memory within cost limits, which is facilitated by techniques like cache and virtual memory.

>[!note]  Measures of Memory Speed
>1. **Memory Access Time**: This is the time between the start of a memory operation and its completion. For example, it is the time between a **Read** command and the **Memory Function Complete (MFC)** signal.
>2. **Memory Cycle Time**: This is the minimum time delay between the start of two independent memory operations. It is typically slightly larger than memory access time. For example, it is the time between two successive memory read operations.

## Memory Cell Organization
A *memory cell array* is a structured arrangement of memory cells designed to store and manage data. ***Each memory cell stores 1 bit of information***
- A memory cell array typically consists of a two-dimensional grid where each cell stores one bit of information. The array is organized into rows and columns, with 2^n rows (where n is the number of address bits) and m columns (representing the number of bits stored per entry, i.e *word length*)
Memory cell arrays can be classified based on their technology:
- **Dynamic Random Access Memory (DRAM)**: Uses capacitors to store bits, requiring periodic refreshing due to charge leakage. It is widely used for main memory in computers due to its high density and cost-effectiveness [4](https://en.wikipedia.org/wiki/DRAM_cell).
- **Static Random Access Memory (SRAM)**: Utilizes flip-flop circuits, providing faster access times and requiring less frequent refreshing compared to DRAM. It is often used for cache memory in processors [4](https://en.wikipedia.org/wiki/DRAM_cell).
- **Read-Only Memory (ROM)**: Stores data permanently and is not meant for modification during normal operation
The primary memory in a computer system is primarily composed of **semiconductor memory**. It's the working memory of the computer where programs and data are stored while the computer is running. Main memory is categorized into RAM and ROM.

- **Rows, Columns, and Word Lines**:
    - Each row of cells in the array forms a memory word. All cells within a row are connected to a common line called the *word line*. The word line is driven by an address decoder on the memory chip.
    - The cells in each column are connected to a *Sense/Write circuit* using two bit lines. These Sense/Write circuits are then connected to the data input/output lines of the chip.

1. **Read Operation**: During a **read operation**, the Sense/Write circuits detect the information stored in the cells that are selected by a word line, and then place this information onto the output data lines.
2. **Write Operation**: During a **write operation**, the Sense/Write circuits take the input data and store that data in the cells that are selected by a word line.

- Example: 16 x 8 Memory Organization:
    - An example of a small memory circuit consists of **16 words, with each word being 8 bits long**, which is known as a **16 x 8 organization**.
    - In this organization, the data input and output of each Sense/Write circuit are connected to a single bidirectional data line. This line can be connected to the data lines of a computer.
    - There are also control lines such as **R/W (Read/Write)**, which specifies the operation needed, and **CS (Chip Select)**, which selects a chip in a multichip memory system.
    - A 16 x 8 memory circuit stores 128 bits and requires 14 external connections for address, data, and control lines, and two lines for power supply and ground.
![[Pasted image 20250131164658.png]]

- Larger Memory Circuits:
    - As memory size increases, more external connections are needed for address, data, and control lines.
    - For example, a 1K memory circuit (1024 memory cells) can be organized as a 128 x 8 memory, which requires a total of 19 external connections.

- Row and Column Addresses:
    - To manage larger memory arrays, the address bits are often divided into two groups to form row and column addresses for the cell array.
    - For instance, a 10-bit address can be divided into two groups of 5 bits each.
    - The row address selects a row of cells, which are accessed in parallel, but only one of these cells is connected to the external data line, based on the column address.
