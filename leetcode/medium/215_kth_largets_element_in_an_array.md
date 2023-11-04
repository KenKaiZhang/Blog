# 215 K<sup>th</sup> Largest Element in an Array

Given an integer array `nums` and an integer `k`, return the `kth` largest element in the array.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Can you solve it without sorting?

## Concept

This is quick select algorithm

Steps

1. Choose a pivot
2. Choose search boundaries `l` and `r`
3. Define `i` where any number below index i is smaller than the pivot
4. Iterate through the list and if number < pivot swap the number with whatever `i` is currently at and increment `i`
5. Swap the pivot with where `i` is
   - This sets the pivot to its final position as if the list was sorted
6. Find the k<sup>th</sup> largest element
   - If `k` is where `i` is then the value in `i` is it
   - Else rerun the algorithm for the section `k` belongs in

_Note: k<sup>th</sup> largest element location on the list should be in `list_size - k`_

## Example

1. Start with the whole array

```
nums = [3,2,1,5,6,4]    l = 0   r = 4   lowB = l = 0    k = 2
```

2. Choose far right as pivot and set any values less than pivot behind the `lowB` and increment `lowB` if swapping occured (up to the pivot)

```
nums = [3,2,1,5,6,4]    l = 0   r = 4   lowB = 3    k = 2
```

3. Swap the pivot with where `lowB` is located

```
nums = [3,2,1,4,6,5]    l = 0   r = 4   lowB = 3    k = 2
```

4. Rerun the algorithm but set `l` to 4 since `list_size - k = 6 - 2 = 4 > lowB`

```
nums = [3,2,1,4,6,5]    l = 4   r = 4   lowB = 4    k = 2
```

5. In this example only one number besides the pivot exists so no numbers are swapped

```
nums = [3,2,1,4,6,5]    l = 4   r = 4   lowB = 4    k = 2
```

6. Swap the pivot with where `lowB` is

```
nums = [3,2,1,4,5,6]    l = 4   r = 4   lowB = 4    k = 2
```

7. Since `list_size - k = 6 - 2 = 4 == lowB`, the answer is `nums[lowB] = 5`

## Code

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        k = len(nums)-k

        def quickSelect(l,r):
            lowB, pivot = l, nums[r]
            for i in range(l,r):
                if nums[i] < pivot:
                    nums[i], nums[lowB] = nums[lowB], nums[i]
                    lowB += 1
            nums[lowB], nums[r] = pivot, nums[lowB]

            if k < lowB: return quickSelect(l, lowB-1)
            elif k > lowB: return quickSelect(lowB+1, r)
            else: return nums[k]

        return quickSelect(0, len(nums)-1)
```

_Note `lowB` indicates the next potential spot for values less than `pivot` and `i` from the for loop indicates the part of the array being traversed_

_Apparently QuickSelect is too slow and we need to use a minheap_

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heap = nums[:k]     # Only keep at most k since that would indicate heap[0] to be kth largest
        heap.heapify(heap)  # Basically sorts the array in ascending order

        for num in nums[k:]:
            # If the number is bigger than the current "answer" add it to the heap (remember it will always be in order since its a heap)
            if num > heap[0]:
                heap.heappop(heap)
                heap.heappush(heap, num)
        return heap[0]
```
