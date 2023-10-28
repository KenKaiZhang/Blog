# 300 Longest Increasing Subsequence

**Medium**

Given an integer array `nums`, return the length of the longest strictly increasing
subsequence.

## Concept

You want to work backwards through the array.

The idea is that for each element, you can decide which prior subsequence you want to attack it to. So if you have an array of 5 and currently on index 2, then you have the option of adding onto the subsequence from index 3 or 4. Of course index 3 can include 4, but we don't know that. You go through this process and then return the max of list generated.

_Remember the list is an indicatore of the longest subsequence possible at index `i`_

## Code

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        # Initialize a dp of 1s since the minimum length for each index of nums will be 1
        LIS = [1] * len(nums)

        # Work backwards
        for i in range(len(nums), -1, -1):
            # Go through the longest subsequence starting from indexs after i
            for j in range(i + 1, len(nums)):
                # Only compare if the current number is less than the previous (due to increasing rule)
                if nums[i] < nums[j]:
                    LIS[i] = max(LIS[i], LIS[j] + 1)

        return max(LIS)
```
