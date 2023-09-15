# 11. Container With Most Water

**Medium**

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

## Concept

Starting on the left and right most heights. This will give us a container with the biggest width. Calculate the volume and save if its the biggest volume found so far. Move left to the right and right to the left depending on which one had the shorter height since changing that will lead to the possibility of finding a taller height. Keep going until left and right meet.

## Example

Assume the given `height` array

```
height = [1,8,6,2,5,4,3,7]  l = 1   r = 7   max = 0
```

Calculate the new volume and check if its a new biggest volume

```
height = [1,8,6,2,5,4,3,7]  l = 1   r = 7   max = 8
```

Move the left pointer to the right since `1 < 7` and repeat the comparison

```
height = [1,8,6,2,5,4,3,7]  l = 8   r = 7   max = 49
```

## Code

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l,r = 0, len(height)-1
        maxVol = 0

        while l < r:
            curVol = min(height[l], height[r]) * (r - l)
            maxVol = max(maxVol, curVol)
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
        return maxVol
```
