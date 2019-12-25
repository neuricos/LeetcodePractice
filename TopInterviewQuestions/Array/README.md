# Array

## Remove Duplicates from Sorted Array

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

### Example 1:

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

### Example 2:

```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

### Clarification:

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

### Solution:

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

### Example 1:

```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

### Example 2:

```
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

### Example 3:

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

### Solution:

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

### Example 1:

```
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

### Example 2:

```
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

**Note:**

- Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
- Could you do it in-place with O(1) extra space?

### Solution:

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

### Example 1:

```
Input: [1,2,3,1]
Output: true
```

### Example 2:

```
Input: [1,2,3,4]
Output: false
```

### Example 3:

```
Input: [1,1,1,3,3,4,3,2,4,2]
Output: true
```

### Solution:

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

### Example 1:

```
Input: [2,2,1]
Output: 1
```

### Example 2:

```
Input: [4,1,2,1,2]
Output: 4
```

### Solution:

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

### Example 1:

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

### Example 2:

```
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

### Solution:

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


