# 80 Remove Duplicates from Sorted Array II

**Medium**

Given an integer array `nums` sorted in non-decreasing order, remove some duplicates in-place such that each unique element appears at most twice. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It does not matter what you leave beyond the first `k` elements.

Return `k` after placing the final result in the first `k` slots of `nums`.

## Concept

The idea is to use two pointers. One that traverses the array and the other that marks where the resulting array should be. The pointer that marks the end of the resulting array will only move under two conditions:

1. The current number has a duplicate count of 2 or less
2. The current number is different than the one observed by the other pointer

## Code

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:

        k = 1
        replace = 0
        current = nums[0]

        for i in range(1, len(nums)):
            # If there are less than 1 duplicate of the current number
            if nums[i] == current and k < 2:
                replace += 1
                k += 1
            # If the current number is unqiue
            elif nums[i] != current:
                replace += 1
                k = 1
                current = nums[i]

            nums[replace] = nums[i]

        return replace + 1
```

**_Condensed version I guess_**

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 0
        for num in nums:
            if i < 2 or num != nums[i-2]:
                nums[i] = num
                i += 1
        return i
```
