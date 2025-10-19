**Goal:** Find the largest sum of a contiguous subarray. (Maximum Subarray Sum)

**Core idea:**
At each element, decide:
* either extend the previous subarray (`current_sum + num`),
* or start fresh from this element (`num`).
Keep track of the best sum seen so far.

> Here’s the setup:  
> We want the **maximum subarray sum** — pick a contiguous chunk of the array that adds up to the biggest total.  
> Example: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]` → the best chunk is `[4, -1, 2, 1]` with sum `6`.
> 
> Kadane’s idea: as you walk through, you carry two trackers:
> - `current_sum` = the best sum ending _at this element_.
> - `best_sum` = the best sum seen anywhere so far.
> 
> Here’s the trick step:  
> when you’re at `nums[i]`, you ask:  
> 👉 “Do I extend the previous subarray (`current_sum + nums[i]`), or start fresh from here (`nums[i]`)? Which gives a bigger sum?”


**Steps:**
1. Initialize
   ```
   current_sum = nums[0]
   best_sum = nums[0]
   ```
2. For each `num` in the rest of the array:
   ```
   current_sum = max(num, current_sum + num)
   best_sum = max(best_sum, current_sum)
   ```
3. Return `best_sum`.

**Edge case:**
* If all numbers are negative → answer is the least negative (largest) element.
**Example:** `[−2, 1, −3, 4, −1, 2, 1, −5, 4]`
* Best subarray is `[4, −1, 2, 1]`, sum = **6**.
**Time complexity:** O(n)
**Space complexity:** O(1)

```al
current_sum = nums[0]
best_sum = nums[0]

for num in nums[]:
    current_sum = max(num, current_sum + num)
    best_sum = max(best_sum, current_sum)

```