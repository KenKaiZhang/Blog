# 424 Longest Repeating Character Replacement

**Medium**

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

## Concept

Since its finding sequence in a string, a **sliding window** will be used. However, due to the condition that characters could be replaced to anything `k` times, sliding window by itself will not work. To get around the condition, a record of number of a times a letter occurs in the current window will be used since given a window where not all the characters are the same, replacing the least common letters with the most common letters will be most optimal.

Everytime the window expands, the new letter is recorded and the condition is checked via `length_of_window - count_of_most_occured` (remember that our record keeps track of all letters in the current window). If the condition does not pass, the window shrinks and the record notes that the dropped character count decreased.

## Example

Given `s` and `k`, create a record of the current window

```
s = "ABABBA"  k = 2   record = {}    window = ""
```

Start expanding the window until condition is false

```
s = "ABABBA"  k = 2   record = {A: 1}          window = "A"
s = "ABABBA"  k = 2   record = {A: 1, B: 1}    window = "AB"
s = "ABABBA"  k = 2   record = {A: 2, B: 1}    window = "ABA"
s = "ABABBA"  k = 2   record = {A: 2, B: 2}    window = "ABAB"
s = "ABABBA"  k = 2   record = {A: 2, B: 3}    window = "ABABB"
```

When the condition fails, begin decrementing the window until the condition is true

```
s = "ABABBA"  k = 2   record = {A: 2, B: 3}    window = "ABABB"
s = "ABABBA"  k = 2   record = {A: 1, B: 3}    window = "BABB"
```

Repeat the cycle until end of `s`

```
s = "ABABBA"  k = 2   record = {A: 1, B: 3}    window = "BABBA"
```

Since the window only shrunk when necessary, the solution will just be the window size

## Code

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        occur = {}
        l = 0

        for r in range(len(s)):
            occur[s[r]] = occur.get(s[r], 0) + 1

            if (r - l + 1) - max(occur.values()) > k:
                occur[s[l]] -= 1
                l += 1

    return r - l + 1

```
