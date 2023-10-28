# 12 Integer to Roman

**Medium**

Given an integer `num`, convert it to a roman numeral

## Concept

Make a table that indicates the conversions for roman numerals to integers for `[1000,900,500,400,100,90,50,40,10,9,5,4,1]`. We include numbers like `900` and `400` because those are unique ones where they don't follow the "stack behind the previous number" rule like how `300` is just `CCC`. Go through each key in the conversion table and if that key is less than or equal to `num`, that means we can add it to the result.

- We go through the keys instead of `num` so we don't have to revisit numbers that we already know are too big

## Code

```python
class Solution:
    def intToRoman(self, num: int) -> str:

        # Generates the conversion table
        nums = [1000,900,500,400,100,90,50,40,10,9,5,4,1]
        romans = ['M','CM','D','CD','C','XC','L','XL','X','IX','V','IV','I']
        itor = {n:r for n,r in zip(nums,romans)}

        res = ""
        for n in itor:
            while n <= num:
                res.append(itor[n])
                nums -= n
        return res
```
