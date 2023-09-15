# 129 Sum Root to Leaf Numbers

**Medium**

You are given the `root` of a binary tree containing digits from 0 to 9 only.

Each root-to-leaf path in the tree represents a number.

For example, the root-to-leaf path `1 -> 2 -> 3` represents the number 123.
Return the total sum of all root-to-leaf numbers. Test cases are generated so that the answer will fit in a 32-bit integer.

## Concept

This is a DFS problem since each root-to-leaf value is a number from root to the deepest possible leaf.

The terminating condition would just be if `root` is `None`.

In the DFS, we are going to pass the current node and the sum up to the point. As the algorithem traverses the list, it will create the number and when it hit a end (a node without children), it'll start adding the left and right together.

## Code

```python
lass Solution:
    def sumNumbers(self, root: Optional[TreeNode]) -> int:

        def dfs(root, num):
            if not root:
                return 0

            num = num * 10 + root.val
            if not root.left and not root.right:
                return num
            return dfs(root.left, num) + dfs(root.right, num)
        return dfs(root, 0)

```
