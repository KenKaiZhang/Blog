# 915 Partition Arrays Into Disjoint Variables

**Medium**

Given an integer array nums, partition it into two (contiguous) subarrays `left` and `right` so that:

- Every element in `left` is less than or equal to every element in `right`.
- `left` and `right` are non-empty.
- `left` has the smallest possible size.

Return the length of `left` after such a partitioning.

## Concept

The idea is to find two maximums (one for left and right). These maximum should follow the conditions:

- No element on the right side of the right maximum should be less than the left maximum

We need to check the whole array so while iterating, two things will happen.

1. The right maximum will be the larges value in the array (through comparison)
2. If an element is less than the left maximum, then the left maximum will be set to right maximum
   - We do this because when a left eleement is less than the left maximum, that means the right maximum is wrong and since we know the right is greater than this element (we compare the right max to every element in the array), setting the left maximum to the right one will force this element to be less than the left element.

## Code

```python
class Solution:
    def partitionDisjoint(self, nums: List[int]) -> int:
        left_max, right_max = nums[0]
        partition = 1
        for i in range(1, n):
            right_max = max(right_max, nums[i])
            if nums[i] < left_max:
                left_max = right_max
                partition = i

        return partition + 1
```
