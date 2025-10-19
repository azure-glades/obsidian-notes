**1. Scanning with a tracker**
* Keep a variable as you iterate (`current_max`, `current_min`, etc.).
* Update it whenever a better candidate shows up.
* Example: largest element → `current_max = max(current_max, num)`.

**2. Tracking top-k (leaderboard trick)**
* Maintain multiple variables (`first`, `second`, …).
* On each element:

  * If it beats `first`, demote `first → second`.
  * Else if it beats `second`, update `second`.
* Careful: use **strict comparisons** if you want distinct values.

**3. Kadane’s Algorithm (max subarray sum)**
* Track running best subarray ending at current index.
* Rule:
  ```
  current_sum = max(num, current_sum + num)
  best_sum = max(best_sum, current_sum)
  ```
* Handles negatives: result = least negative element if all are negative.
* Time O(n), space O(1).

**Key mental pattern:**
“Walk through the array. At each step, decide whether to keep going with what I have, or reset and start fresh.”

There are various techniques involving arrays. 
[[Two Pointer]]
[[Sliding Window]]
