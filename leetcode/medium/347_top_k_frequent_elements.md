# 347 Top K Frequent Elements

**Medium**

Given an integer array `nums` and an integer `k`, return the k most frequent elements. You may return the answer in any order.

## Concept

**Use bucket sort**

Initialize a hashmap to record how often a value appears in the array and a 2D array that hosts how numbers that appear index<sup>th</sup> time. Iterate through the numbers once to get the occurences. After getting the occurance, iterate through the occurances and fill in the frequncy array. Once both objects have been filled, work backwards in the frequency array (since bigger index indicates more occurance) and add it to the result until we get `k` elements.

## Example

Given the following array and `k` value, make a hashmap and a freq array where the size is equivilent to the size of `nums` (since you can't have a number that repeats more than the size of the array)

_Note: we plus 1 because we are indexing by 1 not 0_

```
nums = [1,1,1,2,2,3]    k = 2
occur = {}  freq = [[],[],[],[],[],[],[],[]]
```

Iterate through `nums` and fill out `occur`

```
nums = [1,1,1,2,2,3]    k = 2
occur = {1:3, 2:2, 3:3}  freq = [[],[],[],[],[],[],[],[]]
```

Iterate through `occur` and fill out `freq`

```
nums = [1,1,1,2,2,3]    k = 2
occur = {1:3, 2:2, 3:1}  freq = [[],[3],[2],[1],[],[],[],[]]
```

The results will be found in the right most `k` indexes

## Code

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        occur = {}
        freq = [[] for i in range(len(nums)+1)]

        for num in nums:
            occur[num] = occur.get(num, 0) + 1

        for key, val in occur.items():
            freq[val].append(key)

        res = []
        for i in range(len(freq)-1, 0, -1):
            if len(freq[i]) > 0:
                res.extend(freq[i])
                if len(res) == k:
                    return res
```
