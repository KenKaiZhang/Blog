# 47 Permutations II

**Medium**

Given a collection of numbers, `nums`, that might contain duplicates, return all possible unique permutations in any order.

## Concept

It is not possible to do a decision tree based on the raw input nums since you can use items from indexes outside of the current one.

The algorithm involves using a hashmap to keep the count and a backtracking algorithm to add and remove the element from the current working permutation. The base case of the algorithm is when the permutation is of equal length to `nums`. For each **unique** element in `nums`, we start a permuation with it (assuming there is the count for it), and then recur.

**Sorry bad explaination**

## Code

```python
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        res = []
        perm = []
        count = {n:0 for n in nums}

        # Get the count of each unique value in nums
        for n in nums:
            count[n] += 1

        def generate():
            # Add permutation to result when length is hit
            if len(perm) == len(nums):
                res.append(perm)
                return

            for n in count:
                # Only add a number if the count indicates we didn't use all of it already
                if count[n] > 0:
                    perm.append(n)
                    count[n] -= 1

                    generate()

                    perm.pop()
                    count[n] += 1

        generate()
        return res
```
