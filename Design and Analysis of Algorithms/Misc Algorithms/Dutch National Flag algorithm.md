Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.
We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.
You must solve this problem without using the library's sort function. [75. Sort Colors](https://leetcode.com/problems/sort-colors/)
Best solution is the *Dutch national flag algorithm*
- The Dutch National Flag algorithm is a **three-way partitioning** algorithm.
- It **partitions** the array into three sections (for 0s, 1s, and 2s) using pointers in a **single linear scan**.
- It does **not** use recursion, nor does it process or combine subproblems.
- All changes happen in place, with constant space and a single pass.
```java
class Solution {
    public void sortColors(int[] nums) {
        int low = 0, mid = 0, high = nums.length-1;
        while(mid <= high){
            if(nums[mid] == 0){
                int temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;
                low++;
                mid++;
            }else if(nums[mid] == 1){
                mid++;
            }else{
                int temp = nums[mid];
                nums[mid] = nums[high];
                nums[high] = temp;
                high--;
            }
        }
    }
}
```

- **In-place:** It sorts the array without using any extra space (O(1) additional space).
- **One-pass:** It only makes a single pass through the array (O(n) time).
- **Efficient swaps:** Swapping elements as needed ensures all 0s move left, all 2s move right, and 1s naturally fall in the middle.
- **No auxiliary arrays:** All rearrangements happen inside the input array.
More efficient than counting sort