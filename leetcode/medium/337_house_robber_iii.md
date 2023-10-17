# 337 House Robber III

**Medium**

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called `root`.

Besides the `root`, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if two directly-linked houses were broken into on the same night.

Given the `root` of the binary tree, return the maximum amount of money the thief can rob without alerting the police.

## Concept

Think about what happens when you are are a node. You have the option to rob the node and skip the children or skip the node and rob or skip the child node. This relation can be saved in an array of size 2 where if we rob the current node, then the total robbed will be `node.val + dp_node.left[1] + dp_node.right[1]` and if we didn't, it'll be `dp_node.left[0] + dp_node.right[0]`. We then return the max between the two options.

```
 input tree                tree:
     3                  [3+3+1,4+5]
    / \                /        \
   4   5            [4,3]      [5,1]
  / \   \          /     \          \
 1   2   1      [1,0]    [2,0]     [1,0]
                / \       /  \        /  \
           [0,0] [0,0] [0,0] [0,0]  [0,0] [0,0]
```

## Code

```python
class Solution:
    def rob(self, root: Optional[TreeNode]) -> int:

        def dfs(root):
            # If there is no root, then we can't rob it or its children
            if not root:
                return (0, 0)

            left = dfs(root.left)
            right = dfs(root.right)

            # We do the max of left + max of right because it shows the best outcome if we choose to skip the current
            return (root.val + left[1] + right[1], max(left[0], left[1]) + max(right[0], right[1]))

        return max(dfs(root))
```
