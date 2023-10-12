# 442 Find All Duplicates in an Array

**Medium**

Given an integer array `nums` of length `n` where all the integers of `nums` are in the range `[1, n]` and each integer appears once or twice, return an array of all the integers that appears twice.

You must write an algorithm that runs in `O(n)` time and uses only constant extra space.

## Concept

Since the numbers in the array will be numbers from the range `1 -> n` and never exceed a count of 2, it is possible to use the index to help determine whether or not a value has been checked. By converting `nums[n]` to `-nums[n]`, if we get a duplicate, the second time `nums[n]` will be visited, it'll be negative, letting us know that its a duplicate.

## Code

```python
class Solution:
    def findDuplicates(self, nums: List[int]) -> List[int]:
        res = []
        for num in nums:
            n = abs(num) - 1
            if nums[n] < 0:
                res.append(abs(num))
            nums[n] *= -1
        return res
```
