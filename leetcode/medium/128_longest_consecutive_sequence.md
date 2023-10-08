# 128 Longest Consecutive Sequence

**Medium**

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in `O(n)` time.

## Concept

Using a set, it makes it faster to verify whether or not a number is in the array.

Realize that we only need to find the lenght of the sequence of `n` if `n` itself is the start of the sequence. This can be done by checking if `n - 1` exists in the array. If we find a start of the sequence, begin counting how far into the sequence traversable.

## Code

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        res = 0
        nums_set = set(nums)

        for n in nums:
            # Check if n is the start of a sequence
            if (n-1) not in nums_set:
                length = 0
                # Incrementing length mimics going length down the sequence from n
                while n + length in nums_set:
                    length += 1
                res = max(res, length)
        return res
```
