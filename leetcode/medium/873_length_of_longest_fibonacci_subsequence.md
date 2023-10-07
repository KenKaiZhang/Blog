# 873 Length of Longest Fibonacci Subsequence

**Medium**

Given a strictly increasing array `arr` of positive integers forming a sequence, return the length of the longest Fibonacci-like subsequence of `arr`. If one does not exist, return 0.

## Concept

The basic concept is to grab every pair and see how far into the fibonacci sequence it can take us. There will be an `a` and a `b` and `c` can be calculated via `a + b`. If `b` is in `arr` then, we can try and find the next number in the sequence.

## Code

```python
class Solution:
    def lenLongestFibSubseq(self, arr: List[int]) -> int:
        N = len(arr)
        s = set(arr)
        maxLen = 0

        for i in range(N):
            for j in range(i + 1, N):
                # The fibonacci sequence starting at arr[i]
                a, b = arr[i], arr[j]
                length = 1

                # Loop until b is no longer in set
                while b in s:
                    c = a + b
                    length += 1
                    maxLen = max(maxLen, length)
                    # Go to the next number in the sequence
                    a, b = b, c


        return maxLen if maxLen >= 3 else 0
```

_Note_: `b` indicates the next number in the sequence starting at `a`
