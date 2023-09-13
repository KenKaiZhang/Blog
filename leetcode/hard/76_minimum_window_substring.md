# 76 Minimum Window Substring

**Hard**

Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window
substring of `s`such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.

## Concept

The problem requires the use of **sliding window** and some form of memeory management to keep track of what letters are found that belong in `t` from `s`. Using a hashtable, it's possible to record the occurances of each letter in `t`. After getting the occurances, a sliding window is implemented to go through the string.

As the window expands to the right, any character that belongs in `t` from `s` is added to a new hashtable that records these duplicate values. When a character is accounted for, update a variable `have` indicating a shared character is found and the occurance matches. Keep expanding the window until all shared charracters have been found.

Once `have` is the same as `need` (the number of **unique** characters), check if the new substring is the smallest so far and save it if so. Begin shrinking the window until `have` is no longer the same as `need` (basically if a character is dropped from the window that was shared with `t`, decrement its counter and check whether or not it has become less than the required, if so then `have` will be decremented as well). Once `have` and `need` don't match, begin expanding the window.

Return the smallest substring found.

## Example

Given `s` and `t`, record the occurance of each letter in `t` and figure out how many unique characters are in `t`

```
s = ADOBECODEBANC   t = ABC   tCount = {A:1, B:1, C:1}    need = 3
```

Begin expanding the window to the right until all characters are present and accounted for

```
sub = A   sCount = {A:1}  have = 0
...
sub = ADOB   sCount = {A:1, B:1}  have = 2
...
sub = ADOBEC   sCount = {A:1, B:1, C:1}  have = 3   NEW SHORTEST FOUND
```

Since a working substring has been found (`have` == `need`), check if the substring is of a new minimum length and begin shrinking the substring until `have` does not equate to `need`

```
sub = DOBEC   sCount = {A:0, B:1, C:1}  have = 2
```

Repeat this process until the right bound of the window finishes the string

```
sub = DOBEC   sCount = {A:0, B:1, C:1}  have = 2
...
sub = DOBECODEBA   sCount = {A:1, B:2, C:1}  have = 3

have == need
sub = OBECODEBA   sCount = {A:1, B:2, C:1}  have = 3
...
sub = ODEBA   sCount = {A:1, B:1, C:0}  have = 2

have != need
sub = ODEBAN   sCount = {A:1, B:1, C:0}  have = 2
sub = ODEBANC   sCount = {A:1, B:1, C:1}  have = 3

have == need
sub = DEBANC   sCount = {A:1, B:1, C:1}  have = 3
...
sub = BANC   sCount = {A:1, B:1, C:1}  have = 3     NEW SHORTEST FOUND
sub = ANC   sCount = {A:1, B:0, C:1}  have = 2

have != need
FINISH
```

## Code

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        tCount = {}
        for c in t: tCount[c] = tCount.get(c, 0) + 1

        word, wordLen = "", float("inf")
        have, need = 0, len(tCount)

        l = 0
        sCount = {}

        for r in range(len(s)):
            if s[r] in tCount:
                sCount[s[r]] = sCount.get(s[r], 0) + 1
                if sCount[s[r]] == tCount[s[r]]:
                    have += 1

            while l <= r and have == need:
                if (r - l + 1) < wordLen:
                    word = s[l:r+1]
                    wordLen = r - l + 1

                if s[l] in sCount:
                    sCount[s[l]] -= 1
                    if sCount[s[l]] < tCount[s[l]]:
                        have -= 1

                l += 1

        return word
```
