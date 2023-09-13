# 240 Search a 2D Matrix II

**Medium**

Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

## Concept

Set `row` and `col` pointers to 0 and `matrix[0]_length - 1` respectively. Run a while loop where as long a both `row` and `col` are in bound, then continue.

- If `matrix[row][col]` equates to `target`, then return `True`.
- If `matrix[row][col]` is greater than `target` then move `col` inwards (-1).
  - This works because the conditions indicates that if `target` is in `matrix`, then all items to the right of it will be bigger
- If `matrix[row][col]` is less than `target` then move `row` downwards (-1).
  - This works because the conditions indicates that if `target` is in `matrix`, then all items above it will be smaller

Continue this until found or if not just return `False`.

## Code

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        row, col = 0, len(matrix[0])
        while row < len(matrix) and col >= 0:
            if target == matrix[row][col]:
                return True
            elif target < matrix[row][col]:
                col -= 1
            else:
                row += 1
        return False
```
