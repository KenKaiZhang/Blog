# Rotate Image

**Medium**

You are given an `n x n` 2D `matrix` representing an image, rotate the image by 90 degrees (clockwise).

## Concept

Better to draw it out.

For every layer, rotate the edges of the matrix first and then start working on the cells on the sides. Repeat before left and right intersect. The replacement should happen in reverse order (bottom left element will be in its position before the top left gets placed).

## Example

Assume the `matrix` and view how it gets rotated per iteration on the outer most layer

```
[1,2,3]      [7,2,1]      [7,4,1]
[4,5,6]  =>  [4,5,6]  =>  [8,5,2]
[7,8,9]      [9,8,3]      [9,6,3]
```

Notice only `n - 1` rotations are made.

Watch [Neetcode's solution](https://www.youtube.com/watch?v=fMSJSS7eO1w) for a better visual

## Code

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        left, right = 0, len(matrix)
        while left < right:
            for i in range(right - left):
                top, bottom = left, right

                # Save the first element since it will be replaced
                topLeft = matrix[top][left + i]

                # bottom left -> top left
                matrix[top][left + i] = matrix[bottom - i][left]

                # bottom right -> bottom left
                matrix[bottom - i][left] = matrix[bottom][right - i]

                # top right -> bottom right
                matrix[bottom][right - i] = matrix[top + i][right]

                # top left -> top right
                matrix[top + i][right] = topLeft

            left += 1
            right -= 1
```
