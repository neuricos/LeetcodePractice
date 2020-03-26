# Two Sum

**Level:** Easy

## Description

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the corr
ect order.
Note that an empty string is also considered valid.


## Example

### Example 1

```text
Input: "()"
Output: true
```

### Example 2

```text
Input: "()[]{}"
Output: true
```

### Example 3

```text
Input: "(]"
Output: false
```

### Example 4

```text
Input: "([)]"
Output: false
```

### Example 5

```text
Input: "{[]}"
Output: true
```

## Solution

```java
import java.util.Stack;
import java.util.Map;

class Solution {
    private static final Map<Character, Character> m;
    static {
        m = new HashMap<>();
        m.put('(', ')');
        m.put('[', ']');
        m.put('{', '}');
    }
    public boolean isValid(String s) {
        Stack<Character> stk = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (m.keySet().contains(c)) {
                stk.push(c);
            } else if (m.values().contains(c)) {
                if (stk.empty() || m.get(stk.peek()) != c)
                    return false;
                stk.pop();
            }
        }
        return stk.empty()? true:false;
    }
}
```

## Score

**Runtime:** 3 ms, faster than 9.21% of Java online submissions for Valid Parentheses.

**Memory Usage:** 34.2 MB, less than 100.00% of Java online submissions for Valid Parentheses.
