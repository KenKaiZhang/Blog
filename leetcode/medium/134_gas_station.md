# 134 Gas Station

**Medium**

There are n gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1. If there exists a solution, it is guaranteed to be unique

## Concept

This requires a greedy algorithm.

Realize that something can be done if we observe the summation of `gas`, `cost`, and both. First realize that sum of `gas` should always be greater than or equal to sum of `cost` since there is no way to do a full iteration if it is not possible to accumulate enough gas to do so. Rest is just knowing the algorithm.

Iterate through an array of `gas + cost` and keep track of a total and when the total begins staying positive, indicating progression. If `gas + cost` at `i` is less than 0, then the total is reset to 0 and start is incremented by, else start stays.

Just observe the code.

## Code

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:

        if sum(gas) < sum(cost):
            return -1

        gains = [g + c for g,c in zip(gas, cost)]
        total, start = 0, 0
        for i in range(len(gains)):
            total += gains[i]
            if total < 0:
                total = 0
                start = i + 1
        return start
```
