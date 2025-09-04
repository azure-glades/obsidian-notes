**Core idea:** reuse work as you move a contiguous window across the array. Don’t recalc from scratch.

#### 1. Fixed-size window

* Window length $k$ is known.
* Build first window (sum, max, whatever).
* Slide → subtract outgoing element, add incoming.
* Track best value.
* **Common Qs:** max sum of size $k$, average of subarrays of size $k$.
* **Template:**

```java
int sum = 0;
for (int i = 0; i < k; i++) sum += arr[i];
int maxSum = sum;
for (int i = k; i < n; i++) {
    sum += arr[i] - arr[i-k];
    maxSum = Math.max(maxSum, sum);
}
```

#### 2. Variable-size window

* Window size not fixed, condition decides it.
* Expand right until condition satisfied.
* Shrink left while condition still true.
* Track best length/value.
* **Common Qs:** smallest subarray ≥ target, longest substring with ≤ K distinct chars.
* **Template:**

```java
int left = 0, sum = 0, ans = n+1;
for (int right = 0; right < n; right++) {
    sum += arr[right];
    while (sum >= target) {
        ans = Math.min(ans, right - left + 1);
        sum -= arr[left++];
    }
}
```

#### 3. Distinction

* **Two pointers:** search/match in sorted arrays (not necessarily contiguous).
* **Sliding window:** track stats on contiguous ranges.