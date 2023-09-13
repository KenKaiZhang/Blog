# 59 Spiral Matrix II

**Medium**

Given a positive integer `n`, generate an `n` x `n` matrix filled with elements from 1 to n<sup>2</sup> in spiral order.

## Concept

The idea is simple, make a n x n matrix and then traverser through it spirally while adding values 1 to `n`. The question just teaches how to traverse a matrix spirally. Basically starting from top left do

1. Move to top right
2. Move to bottom right
3. Move to bottom left
4. Move to top right

All while shrinking the bounds because spiraling to the center involves shrinking the the top, left, right, bottom bounds until there is no where to go.

## Example

Not gonna bother.

## Code

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:

        matrix = [[0 for _ in range(n)] for _ in range(n)]

        top, bot = 0, n-1
        left, right = 0, n-1
        value = 1

        while left <= right:    # top <= bot works as well

            for c in range(left, right+1):
                matrix[top][c] = value
                value += 1
            top += 1

            for r in range(top, bottom+1):
                matrix[r][right] = value
                value += 1
            right -= 1

            for c in range(right, left-1, -1):
                matrix[bot][c] = value
                value += 1
            bot -= 1

            for r in range(bot, top-1, -1):
                matrix[r][left] = value
                value += 1
            left += 1

        return matrix
```
