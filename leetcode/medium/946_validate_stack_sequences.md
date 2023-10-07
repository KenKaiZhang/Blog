# 946 Validate Stack Sequences

**Medium**

Given two integer arrays `pushed` and `popped` each with distinct values, return `true` if this could have been the result of a sequence of push and pop operations on an initially empty stack, or `false` otherwise.

## Concept

Don't overthink the problem.

The idea is to used the `pushed` and `popped` array as instruction on how to create a stack. Go through the `pushed` array and add each element into a `stack` and if we encounter an element in `popped` (in order), start popping from `stack`. If `stack` at the end is empty, then return `true` else `false`.

## Code

```python
class Solution:
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        stack = []
        poppedInd = 0

        for num in pushed:
            # Add each element to our stack
            stack.append(num):

            # If its possible to pop an element (determined by order given in popped) do so
            while stack and stack[-1] == popped[poppedInd]:
                stack.pop()
                poppedInd += 1

        return stack == []
```
