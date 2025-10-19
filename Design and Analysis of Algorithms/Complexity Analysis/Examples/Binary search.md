#sorting
## **1. Classic Binary Search**
Find a target element in a sorted array
```java
int binarySearch(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;  // avoids overflow
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1; // not found
}
```
**LeetCode examples:** 704. Binary Search

---
## **2. First/Last Occurrence**
Find the first or last position of a target in a sorted array with duplicates.
```java
// First occurrence
int firstOccurrence(int[] nums, int target) {
    int left = 0, right = nums.length - 1, result = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            result = mid;
            right = mid - 1;  // move left
        } else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return result;
}

// Last occurrence
int lastOccurrence(int[] nums, int target) {
    int left = 0, right = nums.length - 1, result = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            result = mid;
            left = mid + 1;  // move right
        } else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return result;
}
```
**LeetCode examples:** 34. Find First and Last Position of Element in Sorted Array

---
## **3. Lower Bound / Upper Bound**
* **Lower Bound:** First element >= target
* **Upper Bound:** First element > target
```java
int lowerBound(int[] nums, int target) {
    int left = 0, right = nums.length;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) left = mid + 1; //this condition is imp
        else right = mid;
    }
    return left;
}

int upperBound(int[] nums, int target) {
    int left = 0, right = nums.length;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] <= target) left = mid + 1; //condition is imp
        else right = mid;
    }
    return left;
}
```
**LeetCode examples:** 35. Search Insert Position

---
## **4. Binary Search on Answer (Search Space)**
Used when array isn’t directly searchable, e.g., “minimize max” or “capacity to ship within D days” problems.
This is a one-directional condition, i.e if `mid` satisfies our `isPossible()` condition, then ALL elements to the *right* of `mid` also satisify!
```java
boolean isPossible(int[] nums, int target) {
    // problem-specific condition
}

int binarySearchAnswer(int low, int high, int[] nums) {
    int ans = -1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (isPossible(nums, mid)) {
            ans = mid;
            high = mid - 1; // search in lower half
        } else {
            low = mid + 1;
        }
    }
    return ans;
}
```
**LeetCode examples:**
* 1011\. Capacity To Ship Packages Within D Days
* 875. Koko Eating Bananas

---
## **5. Rotated Sorted Array**
Find target in a rotated sorted array.
```java
int searchRotated(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;

        if (nums[left] <= nums[mid]) { // left half sorted
            if (nums[left] <= target && target < nums[mid]) right = mid - 1;
            else left = mid + 1;
        } else { // right half sorted
            if (nums[mid] < target && target <= nums[right]) left = mid + 1;
            else right = mid - 1;
        }
    }
    return -1;
}
```
**LeetCode examples:**
* 33\. Search in Rotated Sorted Array
* 81. Search in Rotated Sorted Array II (handle duplicates)

---
## **6. Peak Element / Local Maximum**
Find a peak element in an unsorted array where `nums[i] > nums[i-1] && nums[i] > nums[i+1]`.
```java
int findPeakElement(int[] nums) {
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < nums[mid + 1]) left = mid + 1;
        else right = mid;
    }
    return left;
}
```
**LeetCode examples:** 162. Find Peak Element

---
## **7. Special Variations**
### **Search in 2D Matrix**
Matrix treated like 1D array:
```java
int rows = matrix.length, cols = matrix[0].length;
int left = 0, right = rows * cols - 1;
while (left <= right) {
    int mid = left + (right - left) / 2;
    int midVal = matrix[mid / cols][mid % cols];
    if (midVal == target) return true;
    else if (midVal < target) left = mid + 1;
    else right = mid - 1;
}
return false;
```
**LeetCode examples:** 74. Search a 2D Matrix

---

### **Tips & Tricks**

1. Always use `mid = left + (right - left) / 2` to avoid overflow.
2. Decide **inclusive/exclusive** (`<=` vs `<`) based on problem.
3. Think of binary search as **two types**:

   * **Search in array** (find index/value)
   * **Search on answer** (min/max satisfying a condition)
4. Handle duplicates carefully for first/last occurrence problems.
5. When unsure, simulate with small arrays on paper.