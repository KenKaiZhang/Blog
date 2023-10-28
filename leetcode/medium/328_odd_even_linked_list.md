# 328 Odd Even Linked List

**Medium**

# 328 Odd Even Linked List

**Medium**

Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

The first node is considered odd, and the second node is even, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

## Concept

Since the algorithm must use `O(1)` space, that means a multipointer system must be used.

1. Odd pointer to link all the odd-positioned nodes
2. Even pointer for the even ones

At the end of the algorithm, connect them together. There are a few things we need:

1. Pointer that points the the first node of the original linked list
2. Pointer that always pointes to the second node
3. Odd pointer needs to make its way to the end so it can be connected with the even one

## Code

```python
class Solution:
    def oddEvenList(self, head: Optional[ListNode]) -> Optional[ListNode]:

        # It is possible for head to be None
        if not head: return None

        odd = head
        even = evenHead = head.next

        # Makes sure that odd will never be None
        while even and even.next:

            # Connect the current odd node to the next odd node
            odd.next = odd.next.next
            odd = odd.next

            # Connect the current even node to the next even node
            even = even.next.next
            even = even.next

        odd.next = evenHead
        return head
```
