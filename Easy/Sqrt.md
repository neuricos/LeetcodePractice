# Reverse Integer

**Level:** Easy

Implement `int sqrt(int x)`.

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

## Example 1

```text
Input: 4
Output: 2
```

## Example 2

```text
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
```

## Solution

### Complexity Analysis

Time Complexity: `O(log(N))`\
Space Complexity: `O(1)`

```python3
class Solution:
    def mySqrt(self, x: int) -> int:
        if x < 0:
            raise ValueError("Input must be non-negative")

        low, high = 0, x

        while low <= high:
            middle = (low + high) // 2
            value = pow(middle, 2)

            if value == x:
                return middle
            if value > x:
                high = middle - 1
            else:
                low = middle + 1

        return low - 1
```
