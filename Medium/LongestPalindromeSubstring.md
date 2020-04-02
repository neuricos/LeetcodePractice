# Longest Palindrome Substring

**Level:** Medium

## Description

Given a string `s`, find the longest palindromic substring in `s`. You may assume that the maximum length of `s` is 1000.

## Example1

```text
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

## Example2

```text
Input: "cbbd"
Output: "bb"
```

## Solution

```python3
class Solution:
    def getPalindromeLen(self, s: str, left: int, right: int) -> int:
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return right - left - 1

    def longestPalindrome(self, s: str) -> str:
        if s is None or len(s) == 0:
            return ""

        start, end = 0, 0

        for i in range(len(s)):
            l = max(
                self.getPalindromeLen(s, i, i),
                self.getPalindromeLen(s, i, i + 1)
            )

            if l > end - start:
                start = i - (l - 1) // 2
                end = i + l // 2

        return s[start:end+1]
```
