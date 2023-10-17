# 343 Integer Break

**Medium**

Given an integer `n`, break it into the sum of `k` positive integers, where `k >= 2`, and maximize the product of those integers.

Return the maximum product you can get

## Concept

This requires some math and recognition of patterns.

If we look at the break down of the numbers betwen 1 to 10, we see the maximum product of each of them are as follows:

```
10  = 36    = 3 x 3 x 2 x 2
9   = 27    = 3 x 3 x 3
8   = 18    = 3 x 3 x 2
7   = 12    = 3 x 2 x 2
6   = 9     = 3 x 3
5   = 6     = 3 x 2
4   = 4     = 2 x 2
3   = 2
2   = 1
1   = 0
```

As we can see from the pattern, if the numbers are less than 4, the maximum product is `n - 1`. Starting from 4 is where the pattern begins. All `n` between `n` and 5 have a maximum number of multiplying repeating 3s as much as possible until not possible, which we then multiply it by the leftover `n` which will always be less than 4.

_To be honest just look at the code._

## Code

_Better solution with O(1) time and space complexity_

```python
class Solution:
    def integerBreak(self, n: int) -> int:
        if n <= 3: return n-1

        res = 1
        while n > 4:
            res *= 3:
            n -= 3
        return res * n
```

or

```python
class Solution:
    def integerBreak(self, n: int) -> int:

        pre7 = [0, 0, 1, 2, 4, 6, 9]
        if n < 7:
            return pre7[n]

        for i in range(7, n+1):
            pre7.append(3 * pre7[(i - 3)])
        return pre7[-1]
```
