# Palindrome Number

**Level:** Easy

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

## Example 1

```text
Input: 121
Output: true
```

## Example 2

```text
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

## Example 3

```text
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

## Solution

```python3
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0:
            return False

        value = 0
        y = x

        while y != 0:
            value = 10 * value + y % 10
            y //= 10

        return True if value == x else False
```

```c
#include <math.h>

bool isPalindrome(int x){
    if (x < 0) {
        return false;
    }
    int y = x;
    long z = 0;
    while (y != 0) {
        z = 10 * z + (y % 10);
        y /= 10;
    }
    return x == z? true:false;
}
```
