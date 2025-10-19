## 📖 What is Prefix Sum?

**Definition**: A prefix sum array where `prefixSum[i]` contains the sum of all elements from index 0 to i in the original array.

**Formula**: `prefixSum[i] = arr[0] + arr[1] + ... + arr[i]`

## 🎯 Core Concept

```
Original:  [2, 4, 6, 8, 10]
Prefix:    [2, 6, 12, 20, 30]
           ↑  ↑   ↑   ↑    ↑
           2  2+4 2+4+6 ... sum of all
```

## 💡 Key Insight

**Range Sum in O(1)**: Sum of elements from index `i` to `j` = `prefixSum[j] - prefixSum[i-1]`

```
arr = [2, 4, 6, 8, 10]
prefixSum = [2, 6, 12, 20, 30]

Sum from index 1 to 3: [4, 6, 8] = 18
Formula: prefixSum[3] - prefixSum[0] = 20 - 2 = 18 ✓
```

## 🔧 Implementation Patterns

### Pattern 1: Basic Prefix Sum Array

```python
def build_prefix_sum(arr):
    n = len(arr)
    prefix = [0] * n
    prefix[0] = arr[0]
    
    for i in range(1, n):
        prefix[i] = prefix[i-1] + arr[i]
    
    return prefix

def range_sum(prefix, left, right):
    if left == 0:
        return prefix[right]
    return prefix[right] - prefix[left-1]
```

### Pattern 2: Prefix Sum with Dummy 0

```python
def build_prefix_sum_with_dummy(arr):
    n = len(arr)
    prefix = [0] * (n + 1)  # Extra space for dummy 0
    
    for i in range(n):
        prefix[i+1] = prefix[i] + arr[i]
    
    return prefix

def range_sum(prefix, left, right):
    # No need to handle left == 0 case
    return prefix[right+1] - prefix[left]
```

### Pattern 3: Space-Optimized (Modify Original)

```python
def build_prefix_sum_inplace(arr):
    for i in range(1, len(arr)):
        arr[i] += arr[i-1]
    return arr
```

## 🌟 Common Problem Types

### 1. Range Sum Queries

**Problem**: Given array and multiple queries for sum in range [i, j] **Solution**: Build prefix sum once, answer each query in O(1)

### 2. Subarray Sum Equals K

**Problem**: Count subarrays with sum = k **Key Insight**: If `prefixSum[j] - prefixSum[i] = k`, then `prefixSum[i] = prefixSum[j] - k`

```python
def subarraySum(nums, k):
    count = 0
    prefix_sum = 0
    sum_count = {0: 1}  # Handle subarrays starting from index 0
    
    for num in nums:
        prefix_sum += num
        count += sum_count.get(prefix_sum - k, 0)
        sum_count[prefix_sum] = sum_count.get(prefix_sum, 0) + 1
    
    return count
```

### 3. Maximum Subarray Sum ([[Kadane's Algorithm]])

**Problem**: Find maximum sum of any contiguous subarray **Connection**: Track running sum, reset when it becomes negative

```python
def maxSubArray(nums):
    max_sum = current_sum = nums[0]
    
    for i in range(1, len(nums)):
        current_sum = max(nums[i], current_sum + nums[i])
        max_sum = max(max_sum, current_sum)
    
    return max_sum
```

### 4. Binary Array Problems

**Problem**: Find longest subarray with equal 0s and 1s **Trick**: Convert 0s to -1s, then find subarray with sum = 0

```python
def findMaxLength(nums):
    # Convert 0 to -1, then find subarray with sum = 0
    sum_to_index = {0: -1}
    max_len = curr_sum = 0
    
    for i, num in enumerate(nums):
        curr_sum += 1 if num == 1 else -1
        
        if curr_sum in sum_to_index:
            max_len = max(max_len, i - sum_to_index[curr_sum])
        else:
            sum_to_index[curr_sum] = i
    
    return max_len
```

## 🎨 2D Prefix Sum

### Building 2D Prefix Sum

```python
def build_2d_prefix_sum(matrix):
    if not matrix or not matrix[0]:
        return []
    
    rows, cols = len(matrix), len(matrix[0])
    prefix = [[0] * (cols + 1) for _ in range(rows + 1)]
    
    for i in range(1, rows + 1):
        for j in range(1, cols + 1):
            prefix[i][j] = (matrix[i-1][j-1] + 
                          prefix[i-1][j] + 
                          prefix[i][j-1] - 
                          prefix[i-1][j-1])
    
    return prefix
```

### 2D Range Sum Query

```python
def sum_region(prefix, r1, c1, r2, c2):
    # Sum of rectangle from (r1,c1) to (r2,c2)
    return (prefix[r2+1][c2+1] - 
            prefix[r1][c2+1] - 
            prefix[r2+1][c1] + 
            prefix[r1][c1])
```

## 🚨 Common Pitfalls & Edge Cases

### Pitfall 1: Index Out of Bounds

```python
# ❌ Wrong
def range_sum(prefix, left, right):
    return prefix[right] - prefix[left-1]  # What if left = 0?

# ✅ Correct
def range_sum(prefix, left, right):
    if left == 0:
        return prefix[right]
    return prefix[right] - prefix[left-1]
```

### Pitfall 2: Empty Subarrays

```python
# When using hashmap, always initialize with {0: count}
sum_count = {0: 1}  # Handles subarrays starting from beginning
```

### Pitfall 3: Integer Overflow

```python
# For very large sums, consider using appropriate data types
# In Python, integers have arbitrary precision, but in other languages:
# Use long long in C++, long in Java
```

## 📊 Time & Space Complexity

|Operation|Time|Space|
|---|---|---|
|Build prefix sum|O(n)|O(n)|
|Range query|O(1)|-|
|Build 2D prefix|O(m×n)|O(m×n)|
|2D range query|O(1)|-|

## 🎯 LeetCode Problems to Practice

### Beginner

- 303. Range Sum Query - Immutable
- 304. Range Sum Query 2D - Immutable
- 724. Find Pivot Index

### Intermediate

- 560. Subarray Sum Equals K
- 974. Subarray Sums Divisible by K
- 523. Continuous Subarray Sum
- 525. Contiguous Array

### Advanced

- 1074. Number of Submatrices That Sum to Target
- 1292. Maximum Side Length of a Square
- 1031. Maximum Sum of Two Non-Overlapping Subarrays

## 🧠 Mental Model

Think of prefix sum as a **"running total"** that lets you:

1. **Build once**: Calculate all running totals upfront
2. **Query fast**: Use subtraction to get any range sum instantly
3. **Transform problems**: Convert complex subarray problems into simple lookup problems

**Remember**: `prefixSum[j] - prefixSum[i-1]` gives you the sum from index `i` to `j` because you're subtracting "everything before i" from "everything up to j".

## 🔄 Quick Reference

```python
# Basic template for subarray sum problems
def solve_subarray_problem(arr, target):
    prefix_sum = 0
    result = 0
    seen = {0: 1}  # or {0: -1} for index tracking
    
    for i, num in enumerate(arr):
        prefix_sum += num
        
        # Check if (prefix_sum - target) exists
        if (prefix_sum - target) in seen:
            result += seen[prefix_sum - target]
        
        # Update seen with current prefix_sum
        seen[prefix_sum] = seen.get(prefix_sum, 0) + 1
    
    return result
```