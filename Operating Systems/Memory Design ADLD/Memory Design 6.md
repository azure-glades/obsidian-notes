> [!question] A computer has an 8 Gbyte memory with 64 bit word sizes. Each block of memory stores 16 words. The computer has a direct mapped cache of 128 blocks. The computer uses word level addressing. What is the address format. If we change the cache to 4 way set associative cache, what is the new address format.

**Given Parameters:**
- Main Memory: 8 GB (2³³ bytes)
- Word Size: 64 bits = 8 bytes
- Block Size: 16 words
- Cache Size (direct-mapped): 128 blocks
- Addressing: Word-level (not byte-level)

**Step 1: Calculate Total Address Bits**
1. **Total words in memory**:
   - Main Memory = 8 GB = 2³³ bytes
   - Words = (2³³ bytes) / (8 bytes/word) = 2³⁰ words
   - **Address bits** = log₂(2³⁰) = 30 bits

**Step 2: Direct-Mapped Cache Address Format**
1. **Block Offset**:
   - 16 words/block → Offset bits = log₂(16) = **4 bits**.
   
2. **Index** (for direct-mapped cache):
   - 128 blocks → Index bits = log₂(128) = **7 bits**.

3. **Tag**:
   - Remaining bits = Total bits - (Index + Offset) = 30 - (7 + 4) = **19 bits**.

**Direct-Mapped Address Format**:
| Tag (19 bits) | Index (7 bits) | Offset (4 bits) |
|---------------|----------------|-----------------|

**Step 3: 4-Way Set-Associative Cache Address Format**
1. **Number of Sets**:
   - 128 blocks / 4-way = 32 sets → Index bits = log₂(32) = **5 bits**.

2. **Tag**:
   - Remaining bits = 30 - (5 + 4) = **21 bits**.

**4-Way Set-Associative Address Format**:
| Tag (21 bits) | Index (5 bits) | Offset (4 bits) |
|---------------|----------------|-----------------|


**Summary**
1. **Direct-Mapped Cache**:
   - Tag = 19 bits, Index = 7 bits, Offset = 4 bits.

2. **4-Way Set-Associative Cache**:
   - Tag = 21 bits, Index = 5 bits, Offset = 4 bits.

**Key Observations**
- The **Offset** (4 bits) remains the same because the block size (16 words) doesn’t change.
- In set-associative caches, the **Index** decreases because fewer sets are needed (32 sets vs. 128 blocks in direct-mapped).
- The **Tag** increases to compensate for the reduced index bits.

---
> [!question] A computer has a 16 Gbyte memory with 32-bit word sizes. Each block of memory stores 8 words. The computer uses a direct-mapped cache with 256 blocks and word-level addressing. **What is the address format for the direct-mapped cache?** **If the cache is changed to a 2-way set-associative design, what is the new address format?**
> >[!info]- Answer
> > Address size = 32 bits
> > Tag: 21 b, Index: 8 b, Offset: 3 b
>

