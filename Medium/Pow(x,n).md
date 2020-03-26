# Pow(x, n)

**Level:** Medium

## Description

Implement `pow(x, n)`, which calculates `x` raised to the `power n (x^n)`.

## Example 1

```text
Input: 2.00000, 10
Output: 1024.00000
```

## Example 2

```text
Input: 2.10000, 3
Output: 9.26100
```

## Example 3

```text
Input: 2.00000, -2
Output: 0.25000
Explanation: 2^(-2) = 1/2^2 = 1/4 = 0.25
```

**Note:**

- -100.0 < x < 100.0
- n is a 32-bit signed integer, within the range [−2^31, 2^31 − 1]

## Solution

```python3
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if x == 0:
            raise ValueError()
        if n == 0:
            return 1

        product = x
        operations = []

        n_curr = abs(n)
        while n_curr != 1:
            if n_curr % 2 == 0:
                n_curr /= 2
                operations.append(2)
            else:
                n_curr -= 1
                operations.append(1)

        while len(operations) != 0:
            operation = operations.pop()
            if operation == 1:
                product *= x
            else:
                product = product * product

        return product if n > 0 else 1 / product
```
