# 289 Game of Life

**Medium**

The `board` is made up of an `m x n` grid of cells, where each cell has an initial state: live (represented by a 1) or dead (represented by a 0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

1. Any live cell with fewer than two live neighbors dies as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population.
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously. Given the current state of the `m x n` grid `board`, return the next state.

## Concept

Just read the rules, implement them and then use some marker to determine if a cell was originally aa 1 or 0.

## Code

```python
class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        ROW = len(board)
        COL = len(board[0])

        for r in range(ROW):
            for c in range(COL):

                cell = board[r][c]
                neighbors = 0
                for direct in [[0,1],[0,-1],[1,0],[-1,0],[1,1],[1,-1],[-1,1],[-1,-1]]:
                    x,y = direct
                    if 0 <= r + x < ROW and 0 <= c + y < COL:
                        neighbor = board[r+x][c+y]
                        if neighbor in [1,2]:
                            neighbors += 1

                if (cell and neighbors < 2) or (cell and neighbors > 3):
                    board[r][c] = 2
                elif not cell and neighbors == 3:
                    board[r][c] = 3

        for r in range(ROW):
            for c in range(COL):
                if board[r][c] == 2:
                    board[r][c] = 0
                elif board[r][c] == 3:
                    board[r][c] = 1
        return board
```
