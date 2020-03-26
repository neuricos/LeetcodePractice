# Median of Two Sorted Arrays

**Level:** Hard

## Description

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be `O(log(m+n))`.

You may assume nums1 and nums2 cannot be both empty.

## Examples

### Example 1

```text
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

### Example 2

```text
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

## Solution

```python3
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        if len(nums1) < len(nums2):
            A, B = nums1, nums2
        else:
            A, B = nums2, nums1
        m, n = len(A), len(B)

        imin, imax, half_len = 0, m, int((m + n + 1) / 2)

        while imin <= imax:
            i = int((imin + imax) / 2)
            j = half_len - i

            if i < m and B[j - 1] > A[i]:
                imin = i + 1
                continue

            if i > 0 and A[i - 1] > B[j]:
                imax = i - 1
                continue

            if i == 0:
                left_max = B[j - 1]
            elif j == 0:
                left_max = A[i - 1]
            else:
                left_max = max(A[i - 1], B[j - 1])

            if (m + n) % 2 == 1:
                return left_max

            if i == m:
                right_min = B[j]
            elif j == n:
                right_min = A[i]
            else:
                right_min = min(A[i], B[j])

            return (left_max + right_min) / 2
```

## Score

**Runtime:** 96 ms, faster than 65.96% of Python3 online submissions for Median of Two Sorted Arrays.\
**Memory Usage:** 13 MB, less than 100.00% of Python3 online submissions for Median of Two Sorted Arrays.
