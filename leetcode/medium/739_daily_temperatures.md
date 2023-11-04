# 739 Daily Temperatures

**Medium**

Given an array of integers `temperatures` represents the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `ith` day to get a warmer temperature. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

## Concept

Use a stack.

The idea is that the stack will be **monotonically decreasing** meaning all values in the stack will be less than or equal to the value to the left of it. As you traverse through `temperatures`, we chack if the current temperature is greater than the RIGHT most value of the stack. If so, then we add the range into result.

## Code

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        res = [0] * len(temperatures)
        stack = []

        for i, temp in enumerate(temperatures):
            while stack and temperatures[stack[-1]] < temp:
                res[stack[-1]] = i - stack[-1]
                stack.pop()
            stack.append(i)
        return res
```
