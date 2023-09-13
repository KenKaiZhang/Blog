# 373 Find K Pairs with Smallest Sums

**Medium**

You are given two integer arrays `nums1` and `nums2` sorted in non-decreasing order and an integer `k`.

Define a pair `(u, v)` which consists of one element from the first array and one element from the second array.

Return the `k` pairs `(u1, v1), (u2, v2), ..., (uk, vk)` with the smallest sums.

## Concept

By using a heap, it is possible to maintain a priority queue based on the sum of two elements from `nums1` and `nums2`.

The heap is filled with every element with `[nums1[i]+nums[2], 0]` for each element in `nums1`. A while loop continue until `k` pairs are found or the heap is empty. Every iteration of the loop pops the top pair (or the smallest total). The pair is saved to the result and then tested to see there are any other numbers in `num2` that can be used to generate a new total (remember the `1` index of each eleemnt in the heap represents the index of the value in `nums2` used to make the total). If there is, then find the new total, update the index, and push it into the heap (since heap maintains sorted order it will work).

## Example

Given the following `nums1` and `nums2`, intialize and populate the heap

```
nums1 = [1,3,5]     nums2 = [2,4,6]     heap = [[3,0],[5,0],[7,0]]  res = []
```

Take the first item from the heap, save it in result and then check if there are new items in `nums2` that can be used to generate a new total

_Remember pair can be calculated via `sum - nums2[pos]` and `nums2[pos]`_

```
current = [3,0]     heap = [[5,0],[7,0],[5,1]]  res = [[1,2]]   // index 1 exists in nums2
```

Take the first item from the heap, save it in result and then check if there are new items in `nums2` that can be used to generate a new total

_Notice how `[5,1]` was moved to the front indicating a smaller pair is possible_

```
current = [5,0]     heap = [[5,1],[7,0],[7,1]]  res = [[1,2],[3,2]]   // index 1 exists in nums2
```

Repeat this process until there are `k` elements in `res` or the heap becomes empty

## Code

```python
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        res = []
        priority = []

        for x in nums1:
            heapq.heappush(priority, [x + nums2[0], 0])

        while k > 0 and priority:
            summ, pos = heap.heappop(priority)
            res.append([summ-nums2[pos], nums2[pos]])
            if pos + 1 < len(nums2):
                heapq.heappush(priority, [summ-nums2[pos] + nums2[pos + 1], post+1])

            k -= 1
        return res
```
