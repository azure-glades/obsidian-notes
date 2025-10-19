# Sliding Window Method - LeetCode Cheatsheet (Java)

## Core Concept

Find optimal subarray/substring by maintaining a window that slides across the array. Avoid nested loops by expanding/shrinking window intelligently.

## When to Use

- **Subarray/substring** problems with contiguous elements
- **Optimization** problems (min/max length, sum, etc.)
- **Keywords**: "longest", "shortest", "maximum", "minimum", "subarray", "substring"

## Two Main Types

### 1. Fixed Size Window

**Pattern**: Window size is predetermined

```java
// Template
int windowSum = 0;
for (int i = 0; i < k; i++) {
    windowSum += arr[i];
}
int maxSum = windowSum;

for (int i = k; i < arr.length; i++) {
    windowSum = windowSum - arr[i-k] + arr[i];
    maxSum = Math.max(maxSum, windowSum);
}
```

### 2. Variable Size Window

**Pattern**: Window size changes based on condition

#### Expand-Contract Template

```java
int left = 0, right = 0;
while (right < arr.length) {
    // Expand window
    // Add arr[right] to window
    
    while (/* window invalid */) {
        // Contract window
        // Remove arr[left] from window
        left++;
    }
    
    // Update result with current valid window
    right++;
}
```

## Common Problem Patterns

### Maximum/Longest Valid Window

```java
int left = 0, maxLen = 0;
for (int right = 0; right < arr.length; right++) {
    // Add arr[right] to window
    
    while (/* window becomes invalid */) {
        // Remove arr[left] from window
        left++;
    }
    
    maxLen = Math.max(maxLen, right - left + 1);
}
```

### Minimum Window (Target Found)

```java
int left = 0, minLen = Integer.MAX_VALUE;
for (int right = 0; right < arr.length; right++) {
    // Add arr[right] to window
    
    while (/* window contains target */) {
        minLen = Math.min(minLen, right - left + 1);
        // Remove arr[left] from window
        left++;
    }
}
```

## Key Data Structures

- **HashMap**: Character/element frequency tracking
- **HashSet**: Unique elements in window
- **Deque**: Min/max in window (monotonic queue)
- **Variables**: Sum, count, conditions

## Example Problems & Solutions

### 1. Longest Substring Without Repeating Characters

```java
public int lengthOfLongestSubstring(String s) {
    Set<Character> set = new HashSet<>();
    int left = 0, maxLen = 0;
    
    for (int right = 0; right < s.length(); right++) {
        while (set.contains(s.charAt(right))) {
            set.remove(s.charAt(left++));
        }
        set.add(s.charAt(right));
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

### 2. Minimum Window Substring

```java
public String minWindow(String s, String t) {
    Map<Character, Integer> need = new HashMap<>();
    Map<Character, Integer> window = new HashMap<>();
    
    for (char c : t.toCharArray()) {
        need.put(c, need.getOrDefault(c, 0) + 1);
    }
    
    int left = 0, right = 0, valid = 0;
    int start = 0, len = Integer.MAX_VALUE;
    
    while (right < s.length()) {
        char c = s.charAt(right++);
        if (need.containsKey(c)) {
            window.put(c, window.getOrDefault(c, 0) + 1);
            if (window.get(c).equals(need.get(c))) {
                valid++;
            }
        }
        
        while (valid == need.size()) {
            if (right - left < len) {
                start = left;
                len = right - left;
            }
            char d = s.charAt(left++);
            if (need.containsKey(d)) {
                if (window.get(d).equals(need.get(d))) {
                    valid--;
                }
                window.put(d, window.get(d) - 1);
            }
        }
    }
    return len == Integer.MAX_VALUE ? "" : s.substring(start, start + len);
}
```

### 3. Max Sum Subarray of Size K (Fixed Window)

```java
public int maxSumSubarray(int[] arr, int k) {
    int windowSum = 0;
    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    
    int maxSum = windowSum;
    for (int i = k; i < arr.length; i++) {
        windowSum = windowSum - arr[i-k] + arr[i];
        maxSum = Math.max(maxSum, windowSum);
    }
    return maxSum;
}
```

## Common Mistakes to Avoid

1. **Off-by-one errors**: Window size = `right - left + 1`
2. **Forgetting to update result**: Update inside/outside loops correctly
3. **Wrong shrinking condition**: Make sure window becomes valid after shrinking
4. **HashMap key existence**: Use `getOrDefault()` or check `containsKey()`
5. **Integer overflow**: Use `Integer.MAX_VALUE` for initialization

## Time Complexity

- **Fixed window**: O(n)
- **Variable window**: O(n) - each element visited at most twice
- **Space**: O(k) where k is window size or unique elements

## Quick Decision Tree

1. **Fixed size mentioned?** → Use fixed window template
2. **Find longest/maximum?** → Expand until invalid, then contract
3. **Find shortest/minimum?** → Contract while valid, expand when invalid
4. **Need to track frequency?** → Use HashMap
5. **Need to track unique elements?** → Use HashSet