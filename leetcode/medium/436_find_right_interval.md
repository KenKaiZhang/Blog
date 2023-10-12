# 436 Find Right Interval

**Medium**

You are given an array of `intervals`, `where intervals[i] = [starti, endi]` and each `starti` is unique.

The right interval for an interval `i` is an interval `j` such that `startj >= endi` and `startj` is minimized. Note that `i` may equal `j`.

Return an array of right interval indices for each interval `i`. If no right interval exists for interval `i`, then put -1 at index `i`.

## Concept

The algorithm utilizes `bisect_left()` to figure out the index of the right interval using binary search.

Create a dictionary that holds all the starts and their index. Create a interval list that is sorted. Iterate through the original `intervals` and use `bisect_left` to figure out where the interval `[current_end, inf]` resides. If there is a spot for it in `intervals`, then the function will return a value less than the length of `intervals`.

## Code

```python
class Solution:
    def findRightInterval(self, intervals: List[List[int]]) -> List[int]:

        # Create a dictionary of starts:index
        starts = {interval[0]:i for i, interval in enumerate(intervals)}
        # Sort the intervals by start number (intervals[i][0])
        sorted_intervals = sorted(intervals, key=lambda x:x[0])
        res = [-1] * len(intervals)

        # Iterate through the original intervals
        for i, interval in enumerate(intervals):
            # Figure out where [end, inf] can be inserted in the sorted_intervals
            index = bisect_left(sorted_intervals, [interval[1], float("-inf")])
            # If a spot is available, get the start of the interval in index
            if index != len(intervals):
                res[i] = starts[sorted_intervals[index][0]]
        return res
```
