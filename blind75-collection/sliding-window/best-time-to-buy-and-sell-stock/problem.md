# Blind75: Best Time to Buy and Sell Stock

### [⇦ Back to Problem Index](../../index.md)

## Textbook Problem

You are given an integer array `prices` where `prices[i]` is the price of NeetCoin on the `i-th` day.

You may choose a single day to buy one NeetCoin and choose a different day in the future to sell it.

Return the maximum profit you can achieve. You may choose to not make any transactions, in which case the profit would be `0`.

**Example 1:**

-   **Input:** `prices = [10,1,5,6,7,1]`
-   **Output:** `6`
    Explanation: Buy on day `1` (price = 1) and sell on day `4` (price = 7), profit = 7 - 1 = 6.

**Example 2:**

-   **Input:** `prices = [10,8,7,5,2]`
-   **Output:** `0`
    Explanation: No profitable transactions can be made, thus the max profit is `0`.

### Constraints

-   `1 <= len(prices) <= 100`
-   `0 <= prices[i] <= 100`

---

### Approach 1: Single Pass

-   **Time Complexity:** `O(n)`, where `n` is the number of days.
-   **Space Complexity:** `O(1)` as no extra space is used apart from variables.
-   **Description:** This approach involves iterating through the price list while maintaining the minimum price observed so far and the maximum profit achievable. As we iterate, we continuously update the minimum price and calculate the potential profit if we were to sell on the current day, comparing it with the maximum profit observed so far.
-   **Algorithm:**

    1. Initialize `min_price` to a very large value and `max_profit` to 0.
    2. Iterate through each price in `prices`:
        - Update `min_price` to be the minimum of `min_price` and the current price.
        - Calculate the potential profit if selling at the current price, which is `current price - min_price`.
        - Update `max_profit` to be the maximum of `max_profit` and the potential profit.
    3. Return `max_profit`.

```python
def max_profit(prices: List[int]) -> int:
	min_price = float('inf')
	max_profit = 0

	for price in prices:
		min_price = min(min_price, price)
		max_profit = max(max_profit, price - min_price)

	return max_profit
```
