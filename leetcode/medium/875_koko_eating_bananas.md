# 875 Koko Eating Bananas

**Medium**

Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in h hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the minimum integer `k` such that she can eat all the bananas within `h` hours.

## Concept

This is a binary search problem.

The idea is to realize that given `piles`, the worst case scenario is if Koko has to eat at the rate of the largest pile. This will always work because the it will guarantee that Koko will finish eating all the piles in `h` time since `h` will always be greater than the number of piles.

This however does not answer the question since Koko is a little slow.

Now you must realize there is a range at which she can eat the piles and that is from `1 -> max(piles)`. This is because Koko can always eat at 1 banana per hour but that does not guarantee her finishing within `h` time. Now the binary search happens. With this new "array", we have to go through each possible `k` until we find the smallest that will allow Koko to finish her bananas in `h`.

The number of hours it takes for Koko to finish all the piles at `k` speed can be calculated with `bananas_in_pile / k` rounded up for each pile.

```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        l, r = 1, max(piles)    # This is the "array"
        minK = r    # Since worst comes to worst she eats at the max pile

        while l <= r:
            k = (l + r) // 2
            tmpH = sum([math.ceil(p / k) for p in piles])   # Finding number of hours it takes at k speed
            if tmpH <= h:
                minK = min(minK, k)
                r = m + 1
            else:
                l = m -1
        return minK

```
