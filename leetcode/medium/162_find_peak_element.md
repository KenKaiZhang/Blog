# 162 Find Peak Element

A peak element is an element that is strictly greater than its neighbors.

Given a 0-indexed integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that `nums[-1] = nums[n] = -∞`. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in `O(log n)` time.

## Concept

Its basically binary search but the condition to search left or right is deterministic on which side has the larger value

## Code

```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        l, r = 0, len(nums)-1
        while l < r:
            m = (l + r) // 2
            # If the value on the right of mid is greater, then a potential peak is on the right side of the array thus we shift the left pointer otherwise we shift the right
            if nums[m] < nums[m+1]:
                l = m + 1
            else:
                r = m
        return r
```
