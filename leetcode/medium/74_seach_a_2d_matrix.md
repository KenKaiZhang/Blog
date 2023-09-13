# 74 Search a 2D Matrix

**Medium**

You are given an m x n integer matrix matrix with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` if target is in matrix or `false` otherwise.

You must write a solution in O(log(m \* n)) time complexity.

## Concept

Since the 2D matrix is special in the sense that it is sorted from the top left item to the bottom right item, the problem can be solved through **binary search**. Originally, the problem should take O(mlog(n)) since it will take log(n) to check if `target` is in each row given `m` rows. However, because the problem states _**the first integer of each row is greater than the last integer of the previous row**_, the time complexity can be approved to O(logn + logm) since there is no need to go through all rows.

The algorithm treats the problem in two

1. Find the row where the target could potentially be
2. Find the target in the row

Both steps require binary search where the tricky part is binary searching the row. Start with two pointers to `top` and `bottom` rows (which are `0` and `size_of_matrix`). The "middle" row in binary search will simply be the `(top + bottom )/ 2`. To check if `target` could potentially be in the row, just check if its between the first and last element of that row. After the potential row is set, simply run binary search on the row.

## Example

Given the 2D matrix and `target`

```
matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]]    target = 3
```

Start by binary searching the rows to look for the row `target` could potentially be in

```
matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]]    top = 0   bot = 2   mid = 1
```

Since `matrix[mid] = [10,11,16,20]` does not include `target` and is a range of numbers bigger, `bot` can be set to `mid-1`

```
matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]]    top = 0   bot = 0   mid = 0
```

Since `target` is now in `top` and `bottom`, binary search row `mid` and the result should be `True` since `target` is in that row.

## Code

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:

        topR, botR = 0, len(matrix) - 1
        while topR <= botR:
            midR = (topR + botR) // 2
            if target < matrix[midR][0]:
                botR = midR - 1
            elif target > matrix[midR][-1]:
                topR = midR + 1
            else:
                break

        row = (topR + botR) // 2
        l, r = 0, len(matrix[0]) - 1
        while l <= r:
            m = (l + r) // 2
            if target < matrix[row][m]:
                r = m - 1
            elif target > matrix[row][m]:
                l = m + 1
            else:
                return True
        return False
```
