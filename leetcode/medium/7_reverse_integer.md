# 7 Reverse Integer

**Medium**

Given a signed 32-bit integer `x`, return `x` with its digits reversed. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-231, 231 - 1]`, then return 0.

## Concept

There are two ways to do this problem:

1. Using module division and build up the reverser number
2. Convert the int to a string, reverse it, and then convert it back to an int

Both should check if the revere value will be out of bounds before returing.

## Code

_Solution 1_

```python
class Solution:
    def reverse(self, x: int) -> int:
        reverse = 0
        negative = x < 0

        x = abs(x)
        while x != 0:
            reverse = (reverse * 10) + (x % 10)
            if reverse > pow(2, 31)-1 or reverse < pow(-2, 31):
                return 0
            x //= 10

        return -res if negative else res
```

_Solution 2_

```python
class Solution:
    def reverse(self, x: int) -> int:
        reverse = int(str(abs(x))[::-1])
        if reverse > pow(2, 31)-1 or reverse < pow(-2, 31):
            return 0
        return reverse if x > 0 else -reverse
```
