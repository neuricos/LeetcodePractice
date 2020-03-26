# Rotate Array

**Level:** Easy

Given an array, rotate the array to the right by k steps, where k is non-negative.

## Example 1

```text
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

## Example 2

```text
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

**Note:**

- Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
- Could you do it in-place with O(1) extra space?

## Solution

### Complexity Analysis

Time Complexity: `O(N)`\
Space Complexity: `O(1)`

```python3
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """

        k = k % len(nums)

        def reverse(nums, si, ei):
            mi = (ei - si + 1) // 2 + si
            for i in range(si, mi):
                j = si + ei - i
                nums[i], nums[j] = nums[j], nums[i]

        # Step 1: Reverse the entire list
        reverse(nums, 0, len(nums) - 1)

        # Step 2: Reverse the first k elements
        reverse(nums, 0, k - 1)

        # Step 3: Reverse the rest of the elements
        reverse(nums, k, len(nums) - 1)
```
