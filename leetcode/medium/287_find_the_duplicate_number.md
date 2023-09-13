# 287 Find the Duplicate Number

**Medium**

Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

You must solve the problem without modifying the array nums and uses only constant extra space.

## Concept

Use **Floyd's Cycle Detection** algorithm.

This is more of a linked list cycle problem. Start with a fast and slow pointer and let them run until they intersect for the first time (fast increments by two and slow increments by one). After the intersection occurs, start a new slow pointer from the beginning of the list and increment (by one) for both the new and old slow pointer until they intersect.

_Why this works_
Assume...

- `p` represents the distance from the start of the list to the start of the cycle
- `x` represnets the distance from the start of the cycle to the intersection of slow and fast
- `c` represents the length of the cycle

Since fast goes twice as fast as slow, then `2(slow) = fast`.

The number of iterations that `fast` will perform can be represented as `p + c - x + c` since it will traverse `p` to get to the cycle, go through the cycle up to the intersection `c-x`, and then traverse through the cycle again `c`.

The number of iterations that `slow` will perform can be represented as `p + c -x` since it will traverse `p` to get to the cycle and iterate until it hits the intersection `c - x`.

Knowing that, the equation becomes

```
2(p + c - x) = p + 2c - x
=> 2p + 2c - 2x = p + 2c - x
=> p - x = 0
=> p = x
```

The goal is to find the start of the cycle since that is where the duplicate will be located and by through Floyd's algorithm, finding the distance in the cycle where it equates to the distance from the start of the list to the cycle is possible. By using the second slow pointer from the beginning, the original and the new slow pointers will approach the start of the cycle simultaneously, resulting in the cycle entry, thus the duplicate

## Example

Given the list, set a fast and slow pointer

```
nums = [1,3,4,2,2]  slow = 0    fast = 0
```

Iterate until fast and slow end intersect

```
nums = [1,3,4,2,2]  slow = 1    fast = 3
nums = [1,3,4,2,2]  slow = 3    fast = 4
nums = [1,3,4,2,2]  slow = 2    fast = 4
nums = [1,3,4,2,2]  slow = 4    fast = 4
```

Create a new slow pointer

```
nums = [1,3,4,2,2]  slow = 2    slow2 = 0
```

Iterate until the two slow pointers intersect

```
nums = [1,3,4,2,2]  slow = 4    slow2 = 0
nums = [1,3,4,2,2]  slow = 2    slow2 = 1
nums = [1,3,4,2,2]  slow = 4    slow2 = 3
nums = [1,3,4,2,2]  slow = 2    slow2 = 2
```

The value that the two pointers intersect represents the duplicate

## Code

```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:

        slow, fast = 0, 0
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break

        slow2 = 0
        while True:
            slow = nums[slow]
            slow2 = nums[slow]
            if slow == slow2:
                return slow
```
