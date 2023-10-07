# 378 Kth Smallest Element in a Sorted Matrix

Given an n x n `matrix` where each of the rows and columns is sorted in ascending order, return the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

**Medium**

## Concept

This requires a min heap.

Initialize a heap and add the first element from each row into it. Start a while loop that iterates while `k` > 1. On each iteration, pop the first element from the min heap (smallest) and then add its neighbor in the `matrix` into the heap. If this neighbor is the new smallest, it will end up at the beginning of the heap for the next iteration.

## Code

```python
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        minheap = []

        i = 0
        while i < k and i < len(matrix):
            heapq.heappush(heap, (matrix[i][0], i, 0))

        while k > 1:
            k -= 1
            _, row, col = heapq.heappop(heap)
            if col + 1 < len(matrix[0]):
                heapq.heappush(heap, (matrix[i][j+1], i, j+1))
        return heap[0][0]

```
