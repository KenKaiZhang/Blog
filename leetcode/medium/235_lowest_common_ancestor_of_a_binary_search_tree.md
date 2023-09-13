# 235 Lowest Common Ancestor of a Binary Search Tree

**Medium**

Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.

## Concept

On the surface it seems very complicated, but once considered the traites of a **binary search tree**, the problem becomes more simple.

An unique trait of a **binary search tree** is that **ALL** nodes to the left of the parent will be smaller and greater for the right side. Knowing that, it is safe to assume that if `p` and `q` have values that causes them to be on opposite sides of the parent (one is smaller than the parent while the other is greater), then the LCA is the parent. If the both `p` and `q` are smaller than the parent, then the LCA is on the left side otherwise its on the right side.

## Example

Hard to show examples for tree problems

## Code

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        cur = root
        while cur:
            # If both p and q are greater than the parent, then the LCA is somewhere to the right
            if cur.val < p.val and cur.val < q.val:
                cur = cur.right
            # If both p and q are less than the parent, then the LCA is somewhere to the less
            elif cur.val > p.val and cur.val > q.val:
                cur = cur.left
            # If both aren't true, then we have a split
            else:
                return cur
```
