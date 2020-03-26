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

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] ret = new int[2];
        Map<Integer,Integer> h = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int comp = target - nums[i];
            if (h.containsKey(comp)) {
                ret[0] = h.get(comp);
                ret[1] = i;
                if (ret[0] == ret[1])
                    continue;
                return ret;
            }
            h.put(nums[i], i);
        }
        return ret;
    }
}
```