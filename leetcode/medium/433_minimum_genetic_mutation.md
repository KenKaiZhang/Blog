# 433 Minimum Genetic Mutation

**Medium**

A gene string can be represented by an 8-character long string, with choices from `'A'`, `'C'`, `'G'`, and `'T'`.

Suppose we need to investigate a mutation from a gene string startGene to a gene string endGene where one mutation is defined as one single character changed in the gene string.

For example, `"AACCGGTT" --> "AACCGGTA"` is one mutation.
There is also a gene bank bank that records all the valid gene mutations. A gene must be in bank to make it a valid gene string.

Given the two gene strings `startGene` and `endGene` and the gene bank `bank`, return the minimum number of mutations needed to mutate from `startGene` to `endGene`. If there is no such a mutation, return `-1`.

Note that the starting point is assumed to be valid, so it might not be included in the bank.

## Concept

This requires **BFS**.

The idea is starting with `startGene`, make every possible mutations possible from it. If the mutation is new and in `bank`, we add it to the queue along with the number of mutations it took to get there. While the queue is not empty or `startGene == endGene`, it means there is still a chance to mutate to the target and mutation is completeted respectively. Until then, keep popping from the queue, find all possible valid mutations, and add them to the queue.

## Example

Start with the following `startGene`, `endGene` and `bank` and `startGene` being the only item in the queue

- Notice how a counter is added to determine how many steps it took to get from `startGene` to the mutation

```
startGene = "AACCGGTT"    endGene = "AACCGGTA"  bank = ["AACCGGTA","AACCGCTA","AAACGGTA"]   queue=[("AACCGGTT", 0)]
```

Take the first item from the queue and find all valid permutations and add it into the queue

```
currGene = "AACCGGTT"  level = 0    queue = [("AACCGGTA", 1)]
```

Repeat until target is hit or the queue becomes empty

```
currGene = "AACCGGTA"   level = 1   queue = [("AACCGCTA", 2), ("AAACGGTA", 2)]
currGene = "AACCGCTA"   level = 2   queue = [("AAACGGTA", 2)]
currGene = "AAACGGTA"   level = 2   queue = []  // Same as endGene so DONE
```

## Code

```python
class Solution:
    def minMutation(self, startGene: str, endGene: str, bank: List[str]) -> int:

        if endGame not in bank:
            return -1

        queue = collections.deque()
        queue.append((startGene, 0))
        visited = {startGene}

        while queue:
            curGene, level = queue.popLeft()
            if curGene == endGene:
                return level
            for i in range(len(curGene)):
                for c in "ACGT":
                    mutation = curGene[:i] + c + curGene[i+1:]
                    if mutation in bank:
                        queue.append((mutation, level+1))
                        visited.add(curGene)
        return -1
```
