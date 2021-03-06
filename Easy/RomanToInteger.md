# Roman to Integer

**Level:** Easy

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```text
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as XXVII, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

## Example 1

```text
Input: "III"
Output: 3
```

## Example 2

```text
Input: "IV"
Output: 4
```

## Example 3

```text
Input: "IX"
Output: 9
```

## Example 4

```text
Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

## Example 5

```text
Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

## Solution

```python3
class Solution:
    def romanToInt(self, s: str) -> int:
        d = {
            'I': 1,
            'V': 5,
            'X': 10,
            'L': 50,
            'C': 100,
            'D': 500,
            'M': 1000
        }
        tot = 0
        for i, c in enumerate(s):
            v = d[c]
            if i + 1 < len(s):
                cc = s[i + 1]
                if (c == 'I' and (cc == 'V' or cc == 'X')) or \
                    (c == 'X' and (cc == 'L' or cc == 'C')) or \
                    (c == 'C' and (cc == 'D' or cc == 'M')):
                    v *= -1
            tot += v
        return tot
```

```java
class Solution {
    private static final Map<Character, Integer> sbDict;

    static {
        sbDict = new HashMap<>();
        sbDict.put('I', 1);
        sbDict.put('V', 5);
        sbDict.put('X', 10);
        sbDict.put('L', 50);
        sbDict.put('C', 100);
        sbDict.put('D', 500);
        sbDict.put('M', 1000);
    }

    public int romanToInt(String s) {
        int arr[] = new int[s.length()];
        int i, tot = 0;

        for (i = 0; i < arr.length; i++)
            arr[i] = sbDict.get(s.charAt(i));

        for (i = 0; i < arr.length - 1; i++)
            if (arr[i] < arr[i+1])
                arr[i] *= -1;

        for (i = 0; i < arr.length; i++)
            tot += arr[i];

        return tot;
    }
}
```

