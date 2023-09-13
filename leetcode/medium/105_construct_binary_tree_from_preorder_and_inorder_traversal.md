# 105 Construct Binary Tree from Preorder and Inorder Traversal

**Medium**

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return the binary tree.

## Concept

This is a recursive problem.

The idea is to realize what preorder and inorder represent. The preorder list shows the possible root nodes of each level (where the number of root node increase exponentially). The inorder list illustrates which side the nodes are located (left or right). Every recursive iteration is building a subtree where the following these steps:

1. Create the root of the subtree with the firs item in the given preorder
2. Find the `index` of the root in `inorder`
3. Run recursion to build the left and right side of the subtree
   - Left preorder and inorder list should be all nodes to the left of `index`
   - Right preorder and inorder list should be all nodes to the right of `index`

Keep going until either `preordor` or `inorder` are empty.

## Example

Start with a given `preorder` and `inorder`

```
preorder = [3,9,20,15,7]    inorder = [9,3,15,20,7]
```

Begin building the tree

```
tree = 3
left =>     preorder = [9]          inorder = [9]
right =>    preorder = [20, 15, 7]  inorder = [15, 20, 7]
```

LEFT

```
tree = 9
left =>     preorder = []  inorder = []
right =>    preorder = []  inorder = []
```

RIGHT

```
tree = 20
left =>     preorder = [15]  inorder = [15]
right =>    preorder = [17]  inorder = [17]
```

Eventually both LEFT and RIGHT will have empty `preorder` and `inorder`, causing the recursion to end and start returning resulting in the tree `[3,9,20,null,null,15,7]`

## Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if not preorder or not inorder:
            return None

        tree = TreeNode(preorder[0])
        index = inorder.index(preorder[0])
        tree.left = self.buildTree(preorder[1:index+1], inorder[:index])
        tree.right = self.buildTree(preorder[index+1:], inorder[index+1:])
        return tree
```
