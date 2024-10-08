# Blind75: Minimum Window Substring

### [⇦ Back to Problem Index](../../index.md)

## Textbook Problem

Given two strings `s` and `t`, return the shortest substring of `s` such that every character in `t`, including duplicates, is present in the substring. If such a substring does not exist, return an empty string `""`.

You may assume that the correct output is always unique.

**Example 1:**

-   **Input:** `s = "OUZODYXAZV", t = "XYZ"`
-   **Output:** `"YXAZ"`
    Explanation: `"YXAZ"` is the shortest substring that includes `"X"`, `"Y"`, and `"Z"` from string `t`.

**Example 2:**

-   **Input:** `s = "xyz", t = "xyz"`
-   **Output:** `"xyz"`

**Example 3:**

-   **Input:** `s = "x", t = "xy"`
-   **Output:** `""`

### Constraints

-   `1 <= len(s) <= 1000`
-   `1 <= len(t) <= 1000`
-   `s` and `t` consist of uppercase and lowercase letters.

---

### Approach 1: Sliding Window with Frequency Count

-   **Time Complexity:** `O(n + m)`, where `n` is the length of `s` and `m` is the length of `t`.
-   **Space Complexity:** `O(1)`, since the space required to store character counts is limited by the size of the alphabet.
-   **Description:** The sliding window approach is used to find the minimum window in `s` that contains all characters of `t`. Two hash maps are used: one to store the frequency of characters in `t` and the other to track the frequency of characters in the current window of `s`. The window is expanded and contracted dynamically to find the smallest valid substring that contains all characters from `t`.
-   **Algorithm:**

    1. Initialize two hash maps: `count_t` to store the frequency of each character in `t`, and `window` to track the frequency of characters in the current window of `s`.
    2. Initialize two pointers, `l` and `r`, to define the window. Use `have` to count how many characters in `t` are currently satisfied in the window and `need` to store the number of unique characters in `t`.
    3. Expand the window by moving `r` to the right until all characters in `t` are present in the window.
    4. Once the window is valid, try to contract it by moving `l` to the right, updating the minimum window size each time a smaller valid window is found.
    5. Return the smallest valid window substring.

```python
def min_window(s: str, t: str) -> str:
    if t == "":
        return ""

    count_t, window = {}, {}
    for c in t:
        count_t[c] = 1 + count_t.get(c, 0)

    have, need = 0, len(count_t)
    res, res_len = [-1, -1], float("infinity")
    l = 0

    for r in range(len(s)):
        c = s[r]
        window[c] = 1 + window.get(c, 0)

        if c in count_t and window[c] == count_t[c]:
            have += 1

        while have == need:
            if (r - l + 1) < res_len:
                res = [l, r]
                res_len = r - l + 1

            window[s[l]] -= 1

            if s[l] in count_t and window[s[l]] < count_t[s[l]]:
                have -= 1

            l += 1

    l, r = res
    return s[l : r + 1] if res_len != float("infinity") else ""
```
