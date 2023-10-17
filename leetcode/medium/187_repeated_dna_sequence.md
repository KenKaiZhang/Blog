# 187 Repeated DNA Sequences

**Medium**

The DNA sequence is composed of a series of nucleotides abbreviated as `'A'`, `'C'`, `'G'`, and `'T'`.

For example, `"ACGAATTCCG"` is a DNA sequence.
When studying DNA, it is useful to identify repeated sequences within the DNA.

Given a string `s` that represents a DNA sequence, return all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule. You may return the answer in any order.

## Concept

The approach is to just get every 10 letter substring starting at a specific position and see if it has been seen before through a set.

- You can use a hash as well

## Code

```python
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        res, seen = set(), set()
        for i in range(len(s) - 9):
            if s[i:i+10] in seen:
                res.add(s[i:i+10])
            seen.add(s[i:i+10])
        return res
```
