# 462 Minimum Moves to Equal Array Elements II

**Medium**

Given an integer array `nums` of size `n`, return the minimum number of moves required to make all array elements equal.

In one move, you can increment or decrement an element of the array by `1`.

## Concept

To solve the problem, you have to realize that the median of the array will always be the value all other values should work towards. Sort the array first, get the median of the array and then add up how many increments/decrements is needed for each element in the array to reach the median.

## Code

```python
class Solution:
    def minMoves2(self, nums: List[int]) -> int:
        nums.sort()
        median = num[len(nums) // 2]
        count = 0

        for n in nums:
            if n == median:
                continue
            count += abs(n - median)
        return count
```
