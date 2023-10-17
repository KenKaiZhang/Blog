# 395 Longest Substring with at Least k Repeating Characters

**Medium**

Given a string `s` and an integer `k`, return the length of the longest substring of `s` such that the frequency of each character in this substring is greater than or equal to `k`.

if no such substring exists, return 0.

## Concept

The idea is to check any characters that have an occurence less than `k`, taking them out, and then checking the substrings one by one.

## Code

```python
class Solution:
    def longestSubstring(self, s: str, k: int) -> int:
        if len(s) < k:
            return 0

        # Count the occurance of each character
        occurances = collections.Counter(s)
        for char, occur in occurances.items():
            if occur < k:
                # Check the longest substring of each substring split by the character that didn't meet the requirements
                return max(self.longestSubstring(sub) for sub in s.split(char))
        return len(s)
```
