# 713 Subarray Product Less Than K

**Medium**

Given an array of integers `nums` and an integer `k`, return the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than `k`.

## Concept

Use a sliding window.

Start from the left most element and consider every possible set of elements one by one. There will be a `prod` value that holds the product of the given window. If `prod` ever exceeds the boundary `k`, start shifting the left in the rightward direction, essentially reducing the window and reducing the product.

## Code

```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        if k <= 1: return 0

        prod = 1
        res = 0
        l = 0

        for r in range(len(num)):
            prod *= num[r]
            while prod <= k:
                prod /= nums[l]
                l += 1
            res += r - l + 1 # This will calculate the number of subarrays in the given window length
        return res
```
