# 130 Surrounding Regions

**Medium**

Given an m x n matrix board containing `'X'` and `'O'`, capture all regions that are 4-directionally surrounded by `'X'`.

- A region is captured by flipping all `'O'`s into `'X'`s in that surrounded region
- A region is not surrounded if one `'O'` is on the border

## Concept

It is better to consider the problem through **_reverse thinking_**. Instead of **"finding surrounding regions then flip the contents"**, think of it as **"finding the non-surrounding regions and flip everything else"**. This leads to a solution that involves traversing the edge of the board, running dfs on those edges to find the region its associated with, mark the contents of the region with something other than `'X'` and `'O'`, and then solving the problem.

## Example

Given the `board`

```
[["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
```

Traverse through the edges and find the unsurrounded region. In `board` it will be any cells connected to cell (3,1).

```
[["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","T","X","X"]]
```

After marking the unique region with a special character (_in this case `'T`_), traverse the matrix and flip all `'O'` to `'X'` and `'T'` to `'O'`.

```
[["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
```

## Code

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:

        ROWS: int, COLS: int = len(board), len(board[0])
        directions: List[List[int]] = [[1,0],[0,1],[-1,0],[0,-1]]

        def mark_region(r, c) -> None:
            if board[r][c] == "O":
                board[r][c] = "T"
                for x,y in directions:
                    if (0 <= r+x < ROWS) and (0 <= c+y < COLS) and board[r+x][c+y] == "O":
                        mark_region(r+x, c+y)

        for r in range(ROWS):
            mark_region(r, 0)
            mark_region(r, COLS-1)
        for c in range(COLS):
            mark_region(0, c)
            mark_region(ROWS-1, c)

        for r in range(ROWS):
            for c in range(COLS):
                if board[r][c] == "O":
                    board[r][c] = "X"
                if board[r][c] == "T":
                    board[r][c] = "O"
```
