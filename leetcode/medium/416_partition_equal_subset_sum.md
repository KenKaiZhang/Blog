# 416 Partition Equal Subset Sum

**Medium**

Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or `false` otherwise.

## Concept

This is a dynamic programming problem.

First realize that partitioning into two subsets that equate means that the sum of both subset should equal to the sum of `nums`. This means that if the sum of `nums` is odd, then this process is impossible or `False`.

The solution involves working backwards and calculating all potential sums possible at an index. So if given a 4-sized array and at index 3, then the dp should contain 0, `nums[3] + nums[4]`, `nums[3]`, and `nums[4]`. Return `True` if half of `sum(nums)` is in the dp.

## Example

Given a valid (True) `nums`

```
nums = [1,5,11,5]
```

Since the total of `nums` is even, it is possible to partition (not guaranteed)

```
nums = [1,5,11,5]   target = 22 / 11 = 2    dp = {0}
```

Start at the end (bottom up) and calculate all possible sums from index and below

```
index = 3   dp = {0,5}
index = 2   dp = {0, 5, 11, 16}
index = 1   dp = {0, 5, 11, 16, 10, 21}
index = 0   dp = {0, 1, 5, 6, 10, 11, 12, 16, 17, 21, 22}
```

Since 11 can be found in `dp`, return `True`

## Code

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        if sum(nums) % 2:
            return False

        dp = set()
        dp.add(0)

        for i in range(len(nums)-1, -1, -1):
            tmpDP = set()
            for prev in dp:
                tmpDP.add(prev + nums[i])
                tmpDP.add(prev)
            dp = tmpDP
        return sum(nums) // 2 in dp
```
