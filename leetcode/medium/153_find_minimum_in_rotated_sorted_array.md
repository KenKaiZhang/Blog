# 153 Find Minimum in Rotated Sorted Array

**Medium**

Suppose an array of length `n` sorted in ascending order is rotated between 1 and `n` times. For example, the array `nums = [0,1,2,4,5,6,7]` might become:

- `[4,5,6,7,0,1,2]` if it was rotated 4 times.
- `[0,1,2,4,5,6,7]` if it was rotated 7 times.

Notice that rotating an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.

Given the sorted rotated array `nums` of unique elements, return the minimum element of this array.

You must write an algorithm that runs in O(log n) time.

## Concept

Since its a searching problem that is required to be O(log n) run time, it's safe to assume the solution is going to utilize **binary search**. Since the goal is to find the minimum, instead of comparing the middle to a target, it is compared to the `left` and `right` most value. If the middle is less than `right`, then the minimum has to be between `left` and `middle`, else it would be between the element after `middle` and `right`. The minimum value will be the left most value in the bounded binary search zone.

## Example

Given a list `nums` start binary search from the far left and right

```
nums = [3,4,5,1,2]  l = 0   r = 4   m = 2
```

Since 5 is greater than 2, the minimum value has to be between index `m+1` and `r`

```
nums = [3,4,5,1,2]  l = 3   r = 4   m = 3
```

Since 3 is less than 2, the minimum has to be between `l` and `m` and since `l < r` is not true anymore, the loop breaks and `nums[l]` is the minimum

## Code

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        l,r = 0, len(nums)-1

        while l < r:
            m = (l + r) // 2
            if nums[m] < nums[r]:
                r = m
            else:
                l = m + 1
        return nums[l]
```
