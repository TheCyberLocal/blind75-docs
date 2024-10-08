# Blind75: Longest Increasing Subsequence

### [⇦ Back to Problem Index](../../index.md)

## Textbook Problem

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from the given sequence by deleting some or no elements without changing the relative order of the remaining characters.

**Example 1:**

-   **Input**: `nums = [9,1,4,2,3,3,7]`
-   **Output**: `4`
-   **Explanation**: The longest increasing subsequence is `[1,2,3,7]`, which has a length of `4`.

**Example 2:**

-   **Input**: `nums = [0,3,1,3,2,3]`
-   **Output**: `4`

### Constraints

-   `1 <= len(nums) <= 1000`
-   `-1000 <= nums[i] <= 1000`

---

### Approach 1: Dynamic Programming

-   **Time Complexity**: `O(n^2)`
-   **Space Complexity**: `O(n)`
-   **Description**: This approach uses dynamic programming to build up the solution. For each element in the array, it checks all previous elements to determine if it can extend the subsequence. If so, it updates the length of the subsequence ending at that element.
-   **Algorithm**:

    1. Create an array `dp` where `dp[i]` represents the length of the longest increasing subsequence ending at index `i`.
    2. Initialize each `dp[i]` to `1` because the minimum subsequence length at any position is `1`.
    3. For each `i` from `1` to `n`, and for each `j` from `0` to `i - 1`, if `nums[i] > nums[j]`, update `dp[i]` to `max(dp[i], dp[j] + 1)`.
    4. The answer is the maximum value in the `dp` array.

```python
def length_of_LIS(nums: List[int]) -> int:
	n = len(nums)
	dp = [1] * n

	for i in range(1, n):
		for j in range(i):
			if nums[i] > nums[j]:
				dp[i] = max(dp[i], dp[j] + 1)

	return max(dp)
```

---

### Approach 2: Dynamic Programming with Binary Search

-   **Time Complexity**: `O(n log n)`
-   **Space Complexity**: `O(n)`
-   **Description**: This optimized approach uses dynamic programming combined with binary search. Instead of maintaining the `dp` array directly, we maintain a list `tails` where `tails[i]` is the smallest possible end value of an increasing subsequence of length `i + 1`. This list is maintained in sorted order, and binary search is used to find the correct position to replace or extend the subsequence.
-   **Algorithm**:

    1. Create an empty list `tails`.
    2. For each element `num` in `nums`, perform a binary search on `tails` to find the smallest element greater than or equal to `num`.
    3. If such an element exists, replace it with `num`; otherwise, append `num` to `tails`.
    4. The length of `tails` is the length of the longest increasing subsequence.

```python
def length_of_LIS(nums: List[int]) -> int:
	tails = []

	for num in nums:
		left, right = 0, len(tails)

		while left < right:
			mid = (left + right) // 2

			if tails[mid] < num:
				left = mid + 1
			else:
				right = mid

		if right >= len(tails):
			tails.append(num)
		else:
			tails[right] = num

	return len(tails)
```
