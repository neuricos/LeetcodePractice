# Two Sum

**Level:** Easy

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Example

```text
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Solution

-> *One-time Hashtable*

Traverse the list and put visited values into a hash table. Each time when we iterate over a value, we check if the complement is in the table.

### Complexity Analysis

Time Complexity: `O(N)`\
Space Complexity: `O(N)`

```python3
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        visited = {}
        for i, num in enumerate(nums):
            comp = target - num
            if comp in visited:
                return [visited[comp], i]
            visited[num] = i
        raise ValueError("No two sum solution")
```
