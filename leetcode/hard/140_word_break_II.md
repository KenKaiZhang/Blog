# 140 Word Break II

**Hard**

Given a string `s` and a dictionary of strings `wordDict`, add spaces in `s` to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in any order.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

## Concept

Given `s`, check if any words in `wordDict` starts `s`. If the a word is found to start `s`, split the string by that word and run the algorithm on the broken down string until all words in `wordDict` have been tried or the string is `""`. Each recursion should return all possible words creatable given `s`.

## Example

Loop through `wordDict` and find that `cat` starts off `s` and then start the recursion process on the `s` without `cat` in the front

```
s = "catsanddog"    wordDict = ["cat", "cats", "and", "sand", "dog"]
```

The deepest part of the recursion should be here

```
s = ""          return = [""]
```

Walking back from the end of the recursion should result in the word found to start the string added onto whatever combination was found after

```
s = dog         return = dog + dfs("") = dog
```

```
s = sanddog     return = sand + dfs(dog) = sand dog
```

```
s = catsanddog  return = cat + dfs(sanddog) = cat sand dog
```

This process is repeated for every word in `wordDict` at every level

_Note: a memo can help remember any previously seen combinations_

## Code

**Based on problem 139**

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        dp = [[] for _ in range(len(s) + 1)]
        dp[-1] = [""]

        for i in range(len(s)-1, -1, -1):
            for word in wordDict:
                if ((i + len(word)) <= len(s)) and s[i:i+len(word)] == word:
                    for post in dp[i+len(word)]:
                        dp[i].append(word + (" " if post else "") + post)
        return dp[0]
```

**Without memo**

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:

        def dfs(string: str) -> List[str]:
            if not string:
                return [""]

            res = []
            for word in wordDict:
                if string.startswith(word):
                    subStrings = dfs(string[len(word):])

                    for sub in subStrings:
                        res.append(word + (" " if sub else "") + sub)
            return res
        return dfs(s)
```

**With memo**

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:

        memo = {}
        def dfs(string: str) -> List[str]:

            if string in memo:
                return memo[string]

            if not string:
                return [""]

            res = []
            for word in wordDict:
                if string.startswith(word):
                    subStrings = dfs(string[len(word):])

                    for sub in subStrings:
                        res.append(word + (" " if sub else "") + sub)

            memo[string] = res
            return res
        return dfs(s)
```
