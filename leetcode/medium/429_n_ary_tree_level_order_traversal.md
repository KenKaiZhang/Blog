# 429 N-ary Tree Level Order Traversal

**Medium**

Given an n-ary tree, return the level order traversal of its nodes' values.

## Concept

Just a normal BFS traversal through a tree.

## Code

```python
class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        res = []
        queue = collections.deque()
        if root:
            queue.append(root)

        while queue:
            layer = []
            current = [queue.pop for _ in range(len(queue))]

            for node in current:
                if node:
                    layer.append(node.val)
                    for child in node.children:
                        if child:
                            queue.append(child)
            res.append(layer)
        return res
```
