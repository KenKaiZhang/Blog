# 57 Insert Interval

**Medium**

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by start<sub>i</sub> and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

## Concept

While obeserving each interval in `intervals`, there are three conditions to worry about:

1. `newInterval` consists of only values lower than current interval
2. `newInterval` consists of only values higher than current interval
3. `newInterval` overlaps the current interval

If _Case 1_ then add the `newInterval` to the new list of intervals and then attach the rest of the old intervals to it the new list and return.

If _Case 2_ then add the current interval into the new list of intervals and move on to checking the next interval.

If _Case 3_ then set `newInterval` to be a merge of it and the current interval. This can be accomplish by setting the lower bound to be the smaller value between the two and the upper bound the bigger value between the two.

Once all intervals have been checked, add `newInterval` into the new list and then return the new list.

- Note how if `newInterval` is less than the current interval, just return the combination of the new list with the newInterval tact on the the remaining old list. This works because if the `newInterval` is less than the current one, then there is no way for it to be overlapping or bigger than any of the older intervals

## Example

Given `intervals` and `newInterval`

```
intervals = [[1,3],[6,9]]   newInterval = [2,5]     output = []
```

Go through `intervals` and check the three cases. `newInterval` seems to overlap the current, set `newInterval` to be the merge of the two

```
current = [1,3]   newInterval = [1,5]   output = []
```

Moving on to the next interval, `newInterval` is now smaller than the current so add `newInterval` into `output` and tact on the rest of `intervals`

```
current = [6,9]     output = [[1,5]] + [6,9] = [[1,5], [6,9]]
```

## Code

```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        output = []

        for i in range(len(intervals)):
            l, u = intervals[i][0], intervals[i][1]

            # Upper bound of newInterval is less than current lower bound
            if newInterval[1] < l:
                output.append(newInterval)
                return output + intervals[i:]

            # Lower bound of newInterval is greater than current upper bound
            elif newInterval[0] > u:
                output.append(intervals[i])

            # Overlap
            else:
                newInterval = [min(l, newInterval[0]), max(u, newInterval[1])]

        output.append(newInterval)
        return output
```
