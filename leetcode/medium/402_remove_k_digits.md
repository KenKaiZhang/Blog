# 402 Remove K Digits

**Medium**

Given string `num` representing a non-negative integer `num`, and an integer `k`, return the smallest possible integer after removing `k` digits from `num`.

## Concept

This requires the use of a monotonic stack and seeing the greedy algorithm.

A monotonic stack is a stack whose elements stays neutral and increases. It is often used to track the maximum or minimum element in a data set.

Iterate through each element in `num` and attempt to add them to the stack. If there is room to remove (`k > 0`) and the current value is less than the last element in the stack, pop the last element until either conditions are False. Once done, add the new value into the stack and continue.

## Example

Assume the starting string `num` and `k`

```
num = "1432219"    k = 3   stack = []
```

For each element in `num` check the conditions before adding them into the stack

```
curr = 1    stack[1]
curr = 4    stack[1,4]
curr = 3    stack[1,3]  // k = 2 since 3 is not bigger than 4
curr = 2    stack[1,2]  // k = 1 since 2 is not bigger than 3
curr = 2    stack[1,2]  // k = 0 since 2 is not bigger than 2
curr = 1    stack[1,2,1]
curr = 9    stack[1,2,1,9]
```

## Code

```python
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        stack = []
        for d in num:
            while k > 0 and stack and stack[-1] > d:
                stack.pop()
                k -= 1
            stack.append(d)

        stack = stack[:len(stack) - k]  // some k could potentionally not be used
        res = "".join(stack)
        return str(int(res)) if res else "0"
```
