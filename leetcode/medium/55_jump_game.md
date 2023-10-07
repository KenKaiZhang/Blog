# 55 Jump Game

**Medium**

You are given an integer array `nums`. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

## Concept

This will be a greedy solution.

Realize that by moving where each index needs to reach to get to the end, this end or `goal` can be shifted along. If the element in the current index can get to the goal, then the goal can be moved to that index since it indicates if any element AFTER that index can reach that index, it can reach the end of the array.

## Code

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        goal = len(nums) - 1

        for i in range(len(nums)):
            # Its i + nums[i] since its if we can get from the current index to the goal
            if i + nums[i] >= goal:
                goal = i

        return not goal
```
