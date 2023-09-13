# 139 Word Break

**Medium**

Given a string `s` and a dictionary of strings `wordDict`, return true if `s` can be segmented into a space-separated sequence of one or more dictionary words.

_Note that the same word in the dictionary may be reused multiple times in the segmentation._

## Concept

The solution to this problem involves checking each character in `s` and seeing if starting from that character, if there is any way to form a word in `wordDict` and if so, if just given that segment of the string (the smaller problem), would it give a string that results in `True`.

## Example

Given a `s` and `wordDict`, initialize an array to indicate if starting at character `i`, if its possible to meet the condition

- The last element of the array is set to `True` because if the substring starts at the end of the string, then that means everything worked

```
s = "catsandog"     wordDict = ["cat", "sand", "an", "dog"]     dp = [False ... True]
```

Start from the end of the string and work up (bottom-up dynamic programming)

```
dp = [False, False, False, False, False, False, False, False, False, True]
s[8] = "g"

dp = [False, False, False, False, False, False, False, False, False, True]
s[7] = "og"

dp = [False, False, False, False, False, False, True, False, False, True]
s[6] = "dog"

...

dp = [True, False, False, False, True, False, True, False, False, True]
s[0] = "catsandog"
```

To determine if a character can be set to True, itself must be part of a word and whatever word it matches and what's leftover must be marked with a `True`

```
s[0] = c is True because "cats" is a word and that leaves "andog" where s[4] = a is part of word "an" and so on
```

## Code

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [False] * len(s) + 1
        dp[-1] = True

        for i in range(len(s)-1, -1, -1):
            for word in wordDict:
                if ((i + len(word)) <= len(s)) and s[i: i+len(word)] == word:
                    dp[i] = dp[i + len(word)]
                if dp[i]:
                    break
        return dp[0]
```
