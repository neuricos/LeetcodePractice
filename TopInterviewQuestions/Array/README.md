# Array

## Remove Duplicates from Sorted Array

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

### Example 1

```text
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

### Example 2

```text
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

### Clarification

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```text
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

### Solution

```python3
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0

        i = 0
        for j in range(1, len(nums)):
            if nums[i] != nums[j]:
                i += 1
                nums[i] = nums[j]

        return i + 1
```

## Best Time to Buy and Sell Stock II

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

### Example 1

```text
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

### Example 2

```text
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

### Example 3

```text
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

### Solution

```python3
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # Find all ascending ranges
        # Buy at the beginning of each range and sell at the end

        rs = []
        low = 0
        high = 1

        while high < len(prices):
            if prices[high] < prices[high - 1]:
                if high - 1 - low > 0:
                    rs.append((low, high -1))
                low = high
            high += 1

        # If the last range keeps ascending, put this range into the ranges
        if high - 1 - low > 0:
            rs.append((low, high - 1))

        tot = 0

        for low, high in rs:
            tot += prices[high] - prices[low]

        return tot
```

## Rotate Array

Given an array, rotate the array to the right by k steps, where k is non-negative.

### Example 1

```text
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

### Example 2

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

### Solution

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

## Contains Duplicate

Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

### Example 1

```text
Input: [1,2,3,1]
Output: true
```

### Example 2

```text
Input: [1,2,3,4]
Output: false
```

### Example 3

```text
Input: [1,1,1,3,3,4,3,2,4,2]
Output: true
```

### Solution

```python3
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        s = set()

        for num in nums:
            if num in s:
                return True
            s.add(num)

        return False
```

## Single Number

Given a **non-empty** array of integers, every element appears twice except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

### Example 1

```text
Input: [2,2,1]
Output: 1
```

### Example 2

```text
Input: [4,1,2,1,2]
Output: 4
```

### Solution

```python3
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        s = set()

        for num in nums:
            if num in s:
                s.remove(num)
            else:
                s.add(num)

        return s.pop()
```

## Intersection of Two Arrays II

Given two arrays, write a function to compute their intersection.

### Example 1

```text
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

### Example 2

```text
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
```

**Note:**

- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.

**Follow up:**

- What if the given array is already sorted? How would you optimize your algorithm?
- What if nums1's size is small compared to nums2's size? Which algorithm is better?
- What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

### Solution

```python3
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        d1 = {}
        d2 = {}
        ret = []

        for num in nums1:
            if num not in d1:
                d1[num] = 0
            d1[num] += 1

        for num in nums2:
            if num not in d2:
                d2[num] = 0
            d2[num] += 1

        for k in d1:
            if k in d2:
                times = min(d1[k], d2[k])
                ret.extend([k for _ in range(times)])

        return ret
```

## Plus One

Given a **non-empty** array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

### Example 1

```text
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

### Example 2

```text
Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```

### Solution

```python3
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        def plusOneHelper(ds: List[int], index: int) -> None:
            if ds[index] == 9:
                ds[index] = 0
                if index == 0:
                    ds.insert(0, 1)
                else:
                    plusOneHelper(ds, index - 1)
            else:
                ds[index] += 1

        l = digits.copy()
        plusOneHelper(l, len(l) - 1)

        return l
```

## Move Zeroes

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

### Example

```text
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note:**

1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.

### Solution

```python3
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """

        def find_zero_index(l: List[int], start: int) -> int:
            i = start
            while i < len(l):
                if l[i] == 0:
                    break
                i += 1
            return i

        zero_index = find_zero_index(nums, 0)
        if zero_index == len(nums):
            # Reached the end
            return

        for j in range(zero_index + 1, len(nums)):
            if nums[j] != 0:
                nums[zero_index], nums[j] = nums[j], 0
                zero_index = find_zero_index(nums, zero_index + 1)
```

## Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have *exactly* one solution, and you may not use the same element twice.

### Example

```text
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### Solution

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

## Valid Sudoku

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated **according to the following rules:**

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the 9 `3x3` sub-boxes of the grid must contain the digits 1-9 without repetition.

![sudoku](./sudoku.png)

A partially filled sudoku which is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.

### Example 1

```text
Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
```

### Example 2

```text
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being 
    modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.
- The given board contain only digits `1-9` and the character `'.'`.
The given board size is always `9x9`.

### Solution

```python3
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        row_dict = {}
        col_dict = {}
        blk_dict = {}

        # Each dict is made up of an index as the key and a set of visited numbers as the value
        # For block dict, the block index is calculated as follows:
        def getBlockIndex(row_index, col_index):
            row = row_index // 3
            col = col_index // 3
            return row + 3 * col

        for row_index in range(len(board)):
            for col_index in range(len(board[0])):
                value = board[row_index][col_index]
                if value != ".":
                    if row_index not in row_dict:
                        row_dict[row_index] = set()
                    if value in row_dict[row_index]:
                        return False
                    row_dict[row_index].add(value)

                    if col_index not in col_dict:
                        col_dict[col_index] = set()
                    if value in col_dict[col_index]:
                        return False
                    col_dict[col_index].add(value)

                    blk_index = getBlockIndex(row_index, col_index)
                    if blk_index not in blk_dict:
                        blk_dict[blk_index] = set()
                    if value in blk_dict[blk_index]:
                        return False
                    blk_dict[blk_index].add(value)

        return True
```

## Rotate Image

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

**Note:**

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

### Example 1

```text
Given input matrix =
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

### Example 2

```text
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

### Solution

```python3
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """

        # This solution has memory complexity = O(1)

        matrix_len = len(matrix)
        s = matrix_len - 1

        for i in range(matrix_len // 2):
            for j in range(i, s-i):
                swap = matrix[i][j]
                matrix[i][j] = matrix[s-j][i]
                matrix[s-j][i] = matrix[s-i][s-j]
                matrix[s-i][s-j] = matrix[j][s-i]
                matrix[j][s-i] = swap
```
