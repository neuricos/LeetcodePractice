# Reverse Integer

**Level:** Easy

Given a 32-bit signed integer, reverse digits of an integer.

## Example 1

```text
Input: 123
Output: 321
```

## Example 2

```text
Input: -123
Output: -321
```

## Example 3

```text
Input: 120
Output: 21
```

**Note:**

Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: `[−2^31, 2^31 − 1]`. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## Solution

```python3
class Solution:
    def reverse(self, x: int) -> int:
        value = 0
        negative = True if x < 0 else False

        if negative:
            x *= -1

        while x != 0:
            value = value * 10 + x % 10
            x //= 10

        if negative:
            value *= -1

        return value if (value >= -(1 << 31) and value <= (1 << 31)) else 0
```
