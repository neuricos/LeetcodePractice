# Implement strStr()

## Description

Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

## Example 1

Input: haystack = "hello", needle = "ll"\
Output: 2

## Example 2

Input: haystack = "aaaaa", needle = "bba"\
Output: -1

## Solution

```java
class Solution {
    public int strStr(String haystack, String needle) {
        char harr[] = haystack.toCharArray();
        char narr[] = needle.toCharArray();

        int hlen = harr.length;
        int nlen = narr.length;

        if (hlen < nlen) return -1;
        if (nlen == 0)   return 0;

        for (int i = 0; i <= hlen - nlen; i++) {
            int j, k;
            for (j = i, k = 0; k < nlen; j++, k++)
                if (harr[j] != narr[k])
                    break;
            if (k == nlen) return i;
        }
        return -1;
    }
}
```

## Score

**Runtime:** 1 ms, faster than 67.76% of Java online submissions for Implement strStr().\
**Memory Usage:** 36.2 MB, less than 100.00% of Java online submissions for Implement strStr().
