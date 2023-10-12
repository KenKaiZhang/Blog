# 767 Reorganize String

**Medium**

Given a string `s`, rearrange the characters of `s` so that any two adjacent characters are not the same.

Return any possible rearrangement of `s` or return `""` if not possible.

## Concept

Start off by keeping track of all occurances of a character in the orginal string. Convert it into a heap so that the character with the highest occurance will be a the front of the heap (this can be done by converting the count to negative so the higher the count, the bigger the negative, the smaller it will be). Set a variable that will hold the "data" of the `previous` charcter.

Create a while loop that loops until both `previous` and the heap are empty. During each iteration, if `previous` is existent and the heap is not, it indicates that the last character added to the string will need to be added to the string AGAIN, failing the algorithm (since there is no other characters). Otherwise, pop from the heap, add the new character to the result and then increment the count (remember we flipped the count to negative). If there was a `previous`, then push it back into the heap since its no longer the last character used. If the current character had a count less than 0, then set that to the previous.

## Code

```python
class Solution:
    def reorganizeString(self, s: str) -> str:
        count = Counter(s)
        maxHeap = [[-cnt, char] for char, cnt in count.items()]
        heapy.heapify(maxHeap)

        prev = None
        res = ""

        while prev or maxHeap:
            # If we added a character last iteration and there is no other characters left, we break
            # This works because prev only holds value if the last used character can still be used
            if prev and not maxHeap:
                return ""

            cnt, char = heap.heappop(maxHeap)
            res += char
            cnt += 1

            # If there was a usable character from the previous iteration, put it back into the heap
            if prev:
                heap.heappush(maxHeap, prev)
                prev = None
            # If the current character can still be used, set it to prev
            if cnt != 0:
                prev = [cnt, char]

        return res
```
