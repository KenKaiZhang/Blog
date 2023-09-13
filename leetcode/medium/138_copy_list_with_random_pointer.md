# 138 Copy List with Random Pointer

**Medium**

Given a linked list where nodes are composed of

```
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
```

where random points to a random node in the linked list, create a deep copy of that list

## Concept

**1. Using a hashmap**

Since indexing a linked list is impossible and `random` could connect to a node that has yet to be created, the list needs to be traversed twice. The first iteration would simply be creating a deep copy of the nodes and the second would be connecting. All deep copies of the nodes will be hosted in hashmap that allows easy access to the nodes.

**2 Using constant space**

The idea is to keep all the copies inside the orginal linked list. After creating a copy, the copy will reside after where the original node and the original nodes `next` will be given to the copy and set to the copy. Setting the `random` feature requires a reitration of the linked list where the copy's (which is always at `original.next`) will be set to the original's `random`'s next since as stated all copies come after the original. After all randoms are set, just disconnect all the originals by setting the copy's `next` to its `next.next`. This requires three iterations of the linked list.

## Example

Given a linked list where `[val, random]`

```
head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
```

Iterate through the linked list and store a deep copy of each node in a hashmap where the `key` is the original node and the `value` is the deep copy

```
To hard to draw out
```

On the second iteration, connect the copied nodes to their proper next and randoms which can be accessed via `map[head.next]` and `map[head.random]`

## Code

```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':

        oldToCopy = {}

        cur = head
        while cur:
            oldToCopy[cur] = Node(cur.val)
            cur = cur.next

        cur = head
        while cur:
            copy = oldToCopy[cur]
            copy.next = oldToCopy[cur.next]
            copy.random = oldToCopy[cur.random]
            cur = cur.next

        return oldToCopy[head]
```

**Constant Space**

```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':

        # making copies and putting them after their original
        # [1 2 3] -> [1 1c 2 2c 3 3c]
        cur = head
        while cur:
            copy = Node(cur.val)
            copy.next = cur.next
            cur.next = copy
            cur = cur.next.next

        # Setting the copies (which can be found in cur's next)
        # to the original's random copy which can be found in
        # random's next
        cur = head
        while cur:
            cur.next.random = cur.random.next if cur.random else None
            cur = cur.next.next

        # Disconnecting the originals and connecting the copies
        # by setting copies (cur.next) to the next copy (cur.next.next.next)
        # A little different since this iteration starts on the 1st copy
        cur = head.next if head else None
        while cur:
            cur.next = cur.next.next if cur.next else None
            cur = cur.next

        return head.next if head else None
```
