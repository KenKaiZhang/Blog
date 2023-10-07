# 120 Triangle

**Medium**

Given a `triangle` array, return the minimum path sum from top to bottom.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

## Concept

This is a dynamic programming problem.

Start from the bottom and work our way up. For every node in every laye in the triangle, set it to the minimum of either the sum of itself and the left value or itself and the right value (so itself and `i` or `i+1`).

## Code

```python
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:

        for i in range(len(triangle)-2, -1, -1):
            for j in range(len(triangle[i])):

                left = triangle[i][j] + triangle[i+1][j]
                right = triangle[i][j] + triangle[i+1][j+1]

                triangle[i][j] = min(left, right)

        return triangle[0][0]
```
