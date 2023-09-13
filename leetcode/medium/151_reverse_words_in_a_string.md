# 151 Reverse Words in a String

Given an input string `s`, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in `s` will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

## Concept

Basically find the word and then build a new string from it.

Start from the beginning of `s` and have a pointer that traverses through until it hits a space. Once a space is hit, add the substring into the new word and move the starting pointer to the other one. Make sure to move the starting pointer to a index with a character every time before doing a traversal.

## Code

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        new_word = ""
        l = 0

        while l < len(s):
            while l < len(s) and s[l] == " ":
                l += 1
            r = l
            while r < len(s) and s[r] != " ":
                r += 1
            if l != r:
                new_word = s[l:r] + " " + new_word
            l = r
        return res[:-1]
```

Or you can use a queue/array and then join the strings after

- Bottom is faster

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        words = collections.deque()
        l = 0

        while l < len(s):
            if s[l] != " ":
                r = l
                while r < len(s) and s[r] != " ":
                    r += 1
                words.appendleft(s[l:r])
                l = r
            l += 1
        return " ".join(words)
```
