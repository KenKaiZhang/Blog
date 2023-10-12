# 835 Image Overlap

**Medium**

You are given two images, `img1` and `img2`, represented as binary, square matrices of size `n x n`. A binary matrix has only 0s and 1s as values.

We translate one image however we choose by sliding all the 1 bits left, right, up, and/or down any number of units. We then place it on top of the other image. We can then calculate the overlap by counting the number of positions that have a 1 in both images.

Note also that a translation does not include any kind of rotation. Any 1 bits that are translated outside of the matrix borders are erased.

Return the largest possible overlap.

## Concept

The idea is to get the locations of all the 1s in both matricies and then using then using that information, find out for each 1 in `img1`, where they can overlap a 1 in `img2`. This can be done by doing creating a unique hash between two points as you will see in the code.

## Code

```python
class Solution:
    def largestOverlap(self, img1: List[List[int]], img2: List[List[int]]) -> int:

        n = len(img1)
        hash = 100
        dict = collections.defaultdict(int)

        ones1, ones2 = [], []

        for r in range(n):
            for c in range(n):
                if img1[r][c]: ones1.append([r,c])
                if img2[r][c]: ones2.append([r,c])

        for o1r, o1c in ones1:
            for o2r, o2c in ones2:
                dict[(o1r - o2r) * hash + (o1c - o2c)] += 1

        return max(dict.values()) if dict else 0
```

_Note_: The formula `(o1r - o2r) * hash + (o1c - o2c)` will create a unique value that will only be achievable by certain combinations of `o1r`, `o1c`, `o2r`, and `o2c`. You can think of the value generated as a id for the transition being made. For example, to get an hash value of -101, it will require that `o1r` and `o2r` to be 1 unit away and `o1c` and `o2c` to be one unit as well. This indicates that the transition of moving right and then down will lead to these two cells to overlap.
