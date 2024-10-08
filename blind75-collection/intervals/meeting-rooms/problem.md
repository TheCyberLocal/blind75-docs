# Blind75: Meeting Rooms

### [⇦ Back to Problem Index](../../index.md)

## Textbook Problem

Given an array of meeting time intervals consisting of start and end times `[[start_1,end_1],[start_2,end_2],...]` where `start_i < end_i`, determine if a person could attend all meetings without any conflicts.

**Example 1:**

-   **Input:** `intervals = [(0,30),(5,10),(15,20)]`
-   **Output:** `False`
-   **Explanation:** The intervals `(0,30)` and `(5,10)` conflict, as do `(0,30)` and `(15,20)`.

**Example 2:**

-   **Input:** `intervals = [(5,8),(9,15)]`
-   **Output:** `True`
-   **Note:** The intervals `(0,8)` and `(8,10)` do not conflict at 8.

### Constraints

-   `0 <= len(intervals) <= 500`
-   `0 <= intervals[i].start < intervals[i].end <= 1,000,000`

---

### Approach 1: Sorting and Checking Overlaps

-   **Time Complexity:** `O(n log n)` where `n` is the number of intervals
-   **Space Complexity:** `O(1)` for sorting in place
-   **Description:** To determine if there are any conflicts between meetings, we can first sort the intervals by their start time. Then, we iterate through the sorted list and check if any two consecutive intervals overlap. If an overlap is found, return `False`. If no overlaps are found, return `True`.
-   **Algorithm:**

    1. If `intervals` is empty, return `True`.
    2. Sort `intervals` by their start times.
    3. Iterate through `intervals` from the second element to the last:
        - If the start time of the current interval is less than the end time of the previous interval, return `False`.
    4. If no overlaps are found during the iteration, return `True`.

```python
def can_attend_meetings(intervals: List[Interval]) -> bool:
	if len(intervals) == 0:
		return True

	intervals.sort(key=lambda i: i.start)

	for i in range(1, len(intervals)):
		i1 = intervals[i - 1]
		i2 = intervals[i]

		if i1.end > i2.start:
			return False
	return True
```
