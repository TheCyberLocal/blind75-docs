# Blind75: Unique Paths

### [⇦ Back to Problem Index](../../index.md)

## Textbook Problem

There is an `m x n` grid where you are allowed to move either down or to the right at any point in time.

Given the two integers `m` and `n`, return the number of possible unique paths that can be taken from the top-left corner of the grid `(grid[0][0])` to the bottom-right corner of the grid `(grid[m - 1][n - 1])`.

You may assume the output will fit in a 32-bit integer.

**Example 1:**

-   **Input**: `m = 3`, `n = 6`
-   **Output**: `21`

**Example 2:**

-   **Input**: `m = 3`, `n = 3`
-   **Output**: `6`

### Constraints

-   `1 <= m, n <= 100`

---

### Approach 1: Dynamic Programming

-   **Time Complexity**: `O(m * n)`
-   **Space Complexity**: `O(n)`
-   **Description**: This approach uses dynamic programming to calculate the number of unique paths in an `m x n` grid. The idea is to iterate over each cell in the grid, and for each cell, the number of unique paths to that cell is the sum of the unique paths to the cell directly above it and the cell directly to the left of it. By using a single array to store the number of paths for the current row, we can optimize the space complexity to `O(n)`, where `n` is the number of columns.
-   **Algorithm**:

    1. Initialize an array `row` of size `n` with all elements set to `1`. This represents the number of unique paths to each cell in the first row.
    2. Iterate through each row from `0` to `m - 2`:
        1. Create a new array `new_row` of size `n`, initialized to `1`.
        2. For each column `j` from `1` to `n - 1` update `new_row[j]` to be the sum of `new_row[j - 1]` and `row[j]`.
        3. Replace `row` with `new_row`.
    3. Return `row[n - 1]`, which contains the number of unique paths to the bottom-right corner of the grid.

```python
def unique_paths(m: int, n: int) -> int:
    row = [1] * n

    for i in range(m - 1):
        new_row = [1] * n

        for j in range(1, n):
            new_row[j] = new_row[j - 1] + row[j]

        row = new_row

    return row[n - 1]
```

---

### Approach 2: Mathematics (Combinatorial Formula)

-   **Time Complexity**: `O(1)`
-   **Space Complexity**: `O(1)`
-   **Description**: This approach leverages a combinatorial formula to calculate the number of unique paths in an `m x n` grid. The problem can be reduced to finding the number of ways to choose `(m - 1)` down moves and `(n - 1)` right moves out of the total `(m + n - 2)` moves. This can be computed using the binomial coefficient, which can be calculated using factorials.
-   **Algorithm**:

    1. Define a helper function `factorial(n)` to compute the factorial of a number `n`.
    2. Compute the number of unique paths using the formula:
       $$\binom{n}{k} = \frac{n!}{k!(n - k)!}$$
    3. Return the result of the above calculation.

```python
def unique_paths(m: int, n: int) -> int:
    def factorial(x):
        if x == 0 or x == 1:
            return 1
        else:
            return x * factorial(x - 1)

    numerator = factorial(m + n - 2)
    denominator = factorial(m - 1) * factorial(n - 1)
    return numerator // denominator
```
