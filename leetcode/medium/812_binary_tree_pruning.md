# 812 Binary Tree Pruning

**Medium**

Given the `root` of a binary tree, return the same tree where every subtree (of the given tree) not containing a 1 has been removed.

## Concept

Think about what happens when its just the nodes 0 -> 1. Since the root's children is 1, the 0 does not get cancelled out. However if its 1 -> 0, then it will. So at what point will the root be terminated?

When iteself is a 0 and its children are non existent.

Using this concept, the recursion will follow two steps:

1. **What is the terminator**: When there the root is `None`.
2. **What gets returned after each iteration**: Whether or not the root should be kept

## Code

```python
class Solution:
    def pruneTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None

         # Check if pruning is needed on the left child
        root.left = self.pruneTree(root.left)
        # Check if pruning is needed on the right child
        root.right = self.pruneTree(root.right)

        # If both children were pruned (no 1s) and the root itself is 0, prune it
        if not root.left and not root.right and not root.val:
            return None

        return root
```
