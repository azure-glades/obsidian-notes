[[Arrays]]
**Purpose:** Efficiently solve problems involving pairs (or subarrays) in sorted arrays or arrays where relative positions matter.

### **Pattern 1: Opposite ends (inwards)**
**Example:** Two-sum in a sorted array
```
nums = [1,3,4,6,8,10], target = 14
```
**Steps:**
1. Set `left = 0`, `right = n-1`.
2. While `left < right`:
   * Compute `sum = nums[left] + nums[right]`.
   * If `sum == target` → solution found.
   * If `sum < target` → move `left` forward (need bigger sum).
   * If `sum > target` → move `right` backward (need smaller sum).
**Result:** `[4,10]`
**Insight:** The limiting factor is the smaller number; move the pointer on the smaller side to increase the sum.

---
### **Pattern 2: Slow-Fast (builder-explorer)**
**Example 1: Remove duplicates from sorted array**
```
nums = [0,0,1,1,1,2,2,3,3,4]
```
* `slow` = last unique element’s index (builder)
* `fast` = scans forward (explorer)
* When `nums[fast] != nums[slow]`, move `slow` forward and copy `nums[fast]`.
**Result:** `[0,1,2,3,4, …]`

**Example 2: Move zeroes to the end**
```
nums = [0,1,0,3,12]
```
* `slow` = next position for nonzero
* `fast` = iterates through array
* When `nums[fast] != 0`, swap `nums[slow]` and `nums[fast]`, then `slow++`.
**Result:** `[1,3,12,0,0]`
**Insight:** One pointer scans, one pointer constructs the target arrangement.

---

## **3-Sum (3-pointer / nested two-pointer)**

**Problem:** Find all unique triplets `(a,b,c)` such that `a+b+c = 0`.
**Example:**
```
nums = [-1,0,1,2,-1,-4]
sorted = [-4,-1,-1,0,1,2]
answer = [[-1,-1,2], [-1,0,1]]
```
**Pattern:** Reduce 3-sum to repeated 2-sum using two pointers.
**Steps:**
1. Sort array.
2. Loop `i = 0..n-3` (fix first element `nums[i]`).
   * Skip duplicates: `if (i > 0 && nums[i] == nums[i-1]) continue`.
3. Set `left = i+1`, `right = n-1`.
4. While `left < right`:
   * Compute `sum = nums[i] + nums[left] + nums[right]`.
   * If `sum == 0`: record triplet, then move pointers past duplicates:
     ```java
     left++; while(left < right && nums[left] == nums[left-1]) left++;
     right--; while(left < right && nums[right] == nums[right+1]) right--;
     ```
   * If `sum < 0` → `left++` (need bigger sum)
   * If `sum > 0` → `right--` (need smaller sum)
**Insight:**
* Outer loop fixes one element.
* Inner two pointers efficiently find pairs that complement it.
* Duplicate checks ensure only unique triplets.

**Example walkthrough:**
```
i=0, nums[i]=-4, left=1, right=5
sum=-4+-1+2=-3 <0 → left++
...
i=1, nums[i]=-1, left=2, right=5
sum=-1+-1+2=0 → record [-1,-1,2], move left/right past duplicates
sum=-1+0+1=0 → record [-1,0,1]
```

**Time complexity:** O(n²), space O(1) extra (ignoring output).
