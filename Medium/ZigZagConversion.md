# ZigZag Conversion

**Level:** Medium

The string "`PAYPALISHIRING`" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```text
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: "`PAHNAPLSIIGYIR`"

Write the code that will take a string and make this conversion given a number of rows:

```text
string convert(string s, int numRows);
```

## Example 1

```text
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

## Example 2

```text
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```

## Solution

### Complexity Analysis

Time Complexity: `O(n)`\
Space Complexity: `O(n)`

```python3
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if len(s) == 0:
            return ""

        if numRows == 1:
            return s

        substrs = ["" for _ in range(numRows)]

        i, s_ptr = 0, 0

        while s_ptr != len(s):
            if i == 0:
                while i < numRows and s_ptr != len(s):
                    substrs[i] += s[s_ptr]
                    i += 1
                    s_ptr += 1
                i = numRows - 2
            else:
                substrs[i] += s[s_ptr]
                s_ptr += 1
                i -= 1

        return "".join(substrs)
```
