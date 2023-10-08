# 230 K<sup>th</sup> Smallest Element in a BST

**Medium**

Given the root of a binary search tree, and an integer `k`, return the `k`<sup>th</sup> smallest value (1-indexed) of all the values of the nodes in the tree.

## Concept

Basically choose a preferred method of traversing the BST in order and when `k` is 0, return the current node's value.

## Code

**_Iterative_**

```python
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        stack = []
        cur = root

        while True:
            if cur:
                stack.append(cur)
                cur = cur.left
            elif stack:
                cur = stack.pop()
                k -= 1
                if k == 0:
                    return cur.val
                cur = cur.right
            else:
                return
``
```

**_Recursively_**

```python
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:

        index = 0
        res = 0

        def traverse(root):
            nonlocal index
            nonlocal res
            if not root:
                return None

            traverse(root.left)
            index += 1
            if index == k:
                res = root.val
                return
            traverse(root.right)

        traverse(root)
        return(res)
```
