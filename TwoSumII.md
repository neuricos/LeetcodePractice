# Two Sum II - Input array is sorted

*Level: Easy*

Given an array of integers that is already **sorted in ascending order**, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

**Note:**

- Your returned answers (both index1 and index2) are not zero-based.
- You may assume that each input would have exactly one solution and you may not use the same element twice.

## Example:

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

## Solution:

Start from the leftmost and rightmost positions. Move the left pointer rightward and right pointer leftward to approach the target value.

### Complexity Analysis

Time Complexity: `O(N)`\
Space Complexity: `O(1)`

```python3
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        i, j = 0, len(numbers) - 1
        while i < j:
            tot = numbers[i] + numbers[j]
            if tot > target:
                j -= 1
            elif tot < target:
                i += 1
            else:
                break
        if numbers[i] + numbers[j] == target:
            return [i + 1, j + 1]
        raise ValueError("No Two Sum II solution")
```