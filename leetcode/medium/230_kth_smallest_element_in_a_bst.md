# 230 K<sup>th</sup> Smallest Element in a BST

**Medium**

Given the root of a binary search tree, and an integer `k`, return the `k`<sup>th</sup> smallest value (1-indexed) of all the values of the nodes in the tree.

## Concept

Easiest method would be to recursively travers through the tree, put values in an array and return the `k`<sup>th</sup> element.

The better solution is to iterativly navigate throught the tree. Start with an empty stack and a pointer to `root`. Move as far left as possible while adding items to the stack. Once it is not possible to move further left, pop from the stack (these will all be the left most values). Keep track of how many values were popped since the number of values popped is similar as to adding a number to the array from left to right. After removing an item from the stack, move the pointer to its right and continue the loop (move to the right because the first pop from the stack will be the far most left item or the smallest item and anything to the right of it will be the next smallest). Once `k` items were popped, whatever node currently on is the solution.

## Code

```python
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        stack = []
        cur = root

        while stack and cur:
            while cur:
                stack.append(cur)
                cur = cur.left
            cur = stack.pop()
            k -= 1
            if k == 0:
                return cur.val
            cur = cur.right
```
