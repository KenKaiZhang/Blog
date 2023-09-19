# 2995 Replace Elements in an Array

**Medium**

You are given a 0-indexed array `nums` that consists of n distinct positive integers. Apply m `operations` to this array, where in the ith operation you replace the number `operations[i][0]` with `operations[i][1]`.

It is guaranteed that in the ith operation:

- `operations[i][0]` exists in `nums`.
- `operations[i][1]` does not exist in `nums`.

Return the array obtained after applying all the operations.

## Concept

Use a dictionary to store information on values in the array and their corresponding index.

## Example

Assume the following `nums` and `operations`

```
nums=[1,2,4,6]    operations=[[1,3],[4,7],[6,1]]
```

The dictionary will be the following

```
nums=[1,2,4,6]    operations=[[1,3],[4,7],[6,1]]    table={1:0, 2:1, 4:2, 6:3}
```

Loop throught `operations` and begin replacing `nums` and adjusting `table accordingly

```
nums=[3,2,4,6]    operations=[[1,3],[4,7],[6,1]]    table={3:0, 2:1, 4:2, 6:3}
nums=[3,2,7,6]    operations=[[4,7],[6,1]]    table={3:0, 2:1, 7:2, 6:3}
nums=[3,2,7,1]    operations=[[6,1]]    table={3:0, 2:1, 7:2, 1:3}
nums=[3,2,7,1]    operations=[]   table={3:0, 2:1, 7:2, 1:3}
```

## Code

```python
class Solution:
    def arrayChange(self, nums: List[int], operations: List[List[int]]) -> List[int]:
        table = {num: i for i, num in enumerate(nums)}

        for original, replacement in operations:
            toReplaceIndex = table[original]
            table[replacement] = table[original]
            del table[original]
            nums[toReplaceIndex] = replacement

        return nums
```
