# 396 Rotate Function

**Medium**

You are given an integer array `nums` of length `n`.

Assume function `F(k) = arr[0] * 0 + arr[1] * 1 + ... +arr[n] * n`. Find the max value of `F(k)` of each rotation of `nums`.

## Concept

This is purly a math problem.

After getting `F(k)` of the orginal array, all other `F(k)` can simply be calculated by taking the previous `F(k)` and adding `sum_of_nums - (length_of_nums * n)` where `n` is each value in `nums` in reversed order.

## Code

```python
class Solution:
    def maxRotateFunction(self, nums: List[int]) -> int:
        f = sum(i * n for i,n in enumerate(nums))
        res = f
        numSum = sum(nums)

        for n in reversed(nums):
            f += numSum - (len(nums) * n)
            res = max(res, f)
        return res
```
