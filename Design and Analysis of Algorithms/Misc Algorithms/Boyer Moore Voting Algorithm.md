[169. Majority Element](https://leetcode.com/problems/majority-element/)
Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array. It is **NOT** the most common element

Solved with the Boyer-Moore Voting algorithm
1. **Candidate & Count:**
    - You keep a “candidate” and a “count”.
2. **Scanning:**
    - You scan the array. If the current number equals the candidate, increase the count.
    - If it’s different, decrease the count.
    - If the count drops to zero, you pick the current number as the new candidate, and reset the count to 1.
3. **Why this works:**
    - The majority element appears more than half the time.
    - Every time you pair a different element with the majority, they “cancel out” in the count.
    - After all cancels, the majority element **cannot** be completely canceled out — it will always be left as the candidate at the end.
# Intuition
- Imagine voting: Every time you see a “vote” for the current candidate, you get stronger (+1).
- Every time you see a “vote” against, you get weaker (–1).
- If you ever run out of support (count = 0), you pick the next candidate to back.
- Since the majority element is more than half, it will always survive all the “cancels”.
# Code
```java
class Solution {
	public int majorityElement(int[] nums) {
		int n = nums.length;
		int maj = nums[0];
		int count = 0;
		for(int i = 0 ; i < n; i++){
			if(nums[i] == maj){
			count++;
			} else {
				count--;
				if(count == 0) {maj = nums[i]; count = 1;}
			}
		}
		return maj;
	}
}
```