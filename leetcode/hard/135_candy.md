# 135 Candy

**Hard**

There are `n` children standing in a line. Each child is assigned a rating value given in the integer array ratings.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.

Return the minimum number of candies you need to have to distribute the candies to the children.

## Concept

Greedy approach

The solution requires checking all the children's left neighbor's ranking compared to itself and then the right neighbor's ranking (so two iterations). On the first iteration (left to right), if the current child's left neighbor has a smaller ranking, give the child the number of candy the neighbor has plus one. After the first iteration do the same thing from right to left. The number of candy that should be given to each child should be the max of each index.

## Example

Create two `ratings` sized arrays

```
ratings = [1,3,2,2,1]   l = [1,1,1,1,1]     r = [1,1,1,1,1]
```

On the first iteration, go through ratings from left to right and compare if the child on the left has a lower rating than it. If so give that child the amount of candy its left neighbor has plus `1`

```
ratings = [1,3,2,2,1]   l = [1,1,1,1,1]     r = [1,1,1,1,1]
ratings = [1,3,2,2,1]   l = [1,2,1,1,1]     r = [1,1,1,1,1]
ratings = [1,3,2,2,1]   l = [1,2,1,1,1]     r = [1,1,1,1,1]
ratings = [1,3,2,2,1]   l = [1,2,1,1,1]     r = [1,1,1,1,1]
ratings = [1,3,2,2,1]   l = [1,2,1,1,1]     r = [1,1,1,1,1]
```

Now do the same thing from right to left

```
ratings = [1,3,2,2,1]   l = [1,1,1,1,1]     r = [1,1,1,1,1]
ratings = [1,3,2,2,1]   l = [1,2,1,1,1]     r = [1,1,1,2,1]
ratings = [1,3,2,2,1]   l = [1,2,1,1,1]     r = [1,1,1,2,1]
ratings = [1,3,2,2,1]   l = [1,2,1,1,1]     r = [1,2,1,2,1]
ratings = [1,3,2,2,1]   l = [1,2,1,1,1]     r = [1,2,1,2,1]
```

The list of given candies should be the max of each index in `l` and `r`

```
res = [1, 2, 1, 2, 1]
```

The minimum number of candies required to satisfy the condition is all the values added up in `res` which is `7`

## Code

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:

        lCandies = [1] * len(ratings)
        rCandies = [1] * len(ratings)

        for i in range(1, len(ratings)):
            if ratings[i] > ratings[i-1]:
                lCandies[i] = lCandies[i-1] + 1

        for i in range(len(ratings)-2, -1, -1):
            if ratings[i] > ratings[i+1]:
                rCandies[i] = rCandies[i+1] + 1

        return sum([max(x,y) for x,y in zip(lCandies, rCandies)])
```

or you can have one array

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:

        candies = [1] * len(ratings)

        for i in range(1, len(ratings)):
            if ratings[i] > ratings[i-1]:
                candies[i] = candies[i-1] + 1

        for i in range(len(ratings)-2, -1, -1):
            if ratings[i] > ratings[i+1]:
                candies[i] = max(candies[i], candies[i+1] + 1)

        return sum(candies)
```
