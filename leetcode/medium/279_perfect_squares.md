# 279 Perfect Squares

**Medium**

Given an integer `n`, return the least number of perfect square numbers that sum to `n`.

## Concept

This is a dynamic programming problem.

The idea is to get the number of perfect squares it takes to create each value from 0 -> `n`. This can be done by iterating through each value (say `i`) and checking between 0 -> `i`, what is the minimum number of ways to add up to `i`. The dynamic programming concept comes in when you realize that a lot of values are being recalculated. If the value 4 was previously calculated to require 1 perfect square (2 \* 2), then why would we recaclulate it when `i` is 8. All values in out dynamic memory should hold the minimum number it takes so if it exists, just go check what it is.

## Example

Given the value `n = 12`, intialize an array `dp` to keep track of progress

- `dp` can be intialzie to any big value, but setting it to `n` is more resonable cuz worse case scenario the number can only be made up of n 1s.
- dp[0] is 0 because there is no perfect square that can produce 0

```
n = 12  dp = [0, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12]
```

Start from 1 and work our way up to 12. `dp[1]` is set to 1 because the only way to make 1 is from 1 \* 1 and there is no other way

```
n = 12 dp = [0, 1, ..., 12]
```

2 is a little special. Since 2 \* 2 results in a value greater than 2, the `dp[2]` is set to the minimum between 12, and `dp[2 - 1] + 1` which gives 2. Now repeat the process.

```
current = 3   dp = [0, 1, 2, 3, 12, 12, 12, 12, 12, 12, 12, 12, 12]
              why: 3 - (1*1) = 3 - 1 = 2 => dp[2] + 1 = 3

current = 4   dp = [0, 1, 2, 3, 1, 12, 12, 12, 12, 12, 12, 12, 12]
              why: 4 - (2*2) = 4 - 4 => dp[0] + 1 = 1

current = 5   dp = [0, 1, 2, 3, 1, 2, 12, 12, 12, 12, 12, 12, 12]
              why: 5 - (2*2) = 5 - 4 => dp[1] + 1 = 2
...

current = 11   dp = [0, 1, 2, 3, 1, 2, 3, 4, 2, 1, 2, 3, 12]
               why: 11 - (3 * 3) = 11 - 9 = 2 => dp[2] + 1 = 3

current = 12   dp = [0, 1, 2, 3, 1, 2, 3, 4, 2, 1, 2, 3, 12]
               why: 12 - (2 * 2) = 12 - 4 = 8 => dp[8] + 1 = 3
                    12 - (3 * 3) = 12 - 9 = 3 => dp[3] + 1 = 4 // not the minimum
```

## Code

```python
class Solution:
    def numSquares(self, n: int) -> int:
        dp = [n for _ in range(n+1)]
        dp[0] = 0

        for current in range(1, n+1):
            for i in range(1, current + 1):
                square = i ** 2
                if current - square < 0:
                    break
                dp[current] = min(dp[current], dp[current - square] + 1)
        return dp[-1]
```
