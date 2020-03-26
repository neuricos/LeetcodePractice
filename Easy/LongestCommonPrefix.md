# Longest Common Prefix

**Level:** Easy

## Description

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

## Example 1

```text
Input: ["flower","flow","flight"]
Output: "fl"
```

## Example 2

```text
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## Solution

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) return "";

        String prefix = "";
        for (int i = 0; i < strs[0].length(); i++) {
            char c = strs[0].charAt(i);
            for (int j = 1; j < strs.length; j++) {
                if (i == strs[j].length() || strs[j].charAt(i) != c) {
                    return prefix;
                }
            }
            prefix += c;
        }

        return prefix;
    }
}
```

## Score

**Runtime:** 1 ms, faster than 74.51% of Java online submissions for Longest Common Prefix.\
**Memory Usage:** 35.8 MB, less than 100.00% of Java online submissions for Longest Common Prefix.
