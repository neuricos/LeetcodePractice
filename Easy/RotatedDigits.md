# Two Sum

**Level:** Easy

## Description

X is a good number if after rotating each digit individually by 180 degrees, we get a valid number that is different from X.  Each digit must be rotated - we cannot choose to leave it alone.

A number is valid if each digit remains a digit after rotation. 0, 1, and 8 rotate to themselves; 2 and 5 rotate to each other; 6 and 9 rotate to each other, and the rest of the numbers do not rotate to any other number and become invalid.

Now given a positive number `N`, how many numbers X from `1` to `N` are good?

## Example

```text
Input: 10
Output: 4
Explanation: 
There are four good numbers in the range [1, 10] : 2, 5, 6, 9.
Note that 1 and 10 are not good numbers, since they remain unchanged after rotating.
```

## Solution

```java
class Solution {
    public int rotatedDigits(int N) {
        int count = 0;
        for (int i = 2; i <= N; i++) {
            int value = i;
            boolean flag = false;
            while (value != 0) {
                int digit = value % 10;
                if (digit == 3 || digit == 4 || digit == 7)
                    break;
                if (digit == 2 || digit == 5 || digit == 6 || digit == 9)
                    flag = true;
                value /= 10;
            }
            if (value != 0 || !flag)
                continue;
            count++;
        }
        return count;
    }
}
```

## Score

**Runtime:** 4 ms, faster than 48.87% of Java online submissions for Rotated Digits.\
**Memory Usage:** 32.9 MB, less than 41.67% of Java online submissions for Rotated Digits.
