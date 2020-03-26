# Longest Substring Without Repeating Characters

**Level:** Medium

## Description

Given a string, find the length of the longest substring without repeating characters.

## Example 1

```text
Input: "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

## Example 2

```text
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

### Example 3

```text
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.

Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## Solution

Time Complexity: `O(n)`\
Space Complexity: `O(n)`

```python3
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if len(s) == 0:
            return 0

        seen_chars = ""
        longest_substr_len = 0

        for c in s:

            if c in seen_chars:
                longest_substr_len = max(longest_substr_len, len(seen_chars))
                repeated_char_index = seen_chars.index(c)
                seen_chars = seen_chars[repeated_char_index + 1:]

            seen_chars = seen_chars + c

        return max(longest_substr_len, len(seen_chars))
```
