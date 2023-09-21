# 1081 Smallest Subsequence of Distince Characters

**Medium**

Given a string `s`, return the lexicographically smallest subsequence of `s` that contains all the distinct characters of `s` exactly once.

## Concept

There are a few things that need to be kept track of:

1. Characters that will form the answer
2. If a character has already been used
3. Character availability

`1.` can be solved by storing the string as an array, making it easy to remove and observe the components of the resulting string. `2.` can be done by intializing an array of length 26 (one for each letter). `3.` be solved with an occurance hashmap.

Any letter in `s` can be a potential for the beginning or a component of the resulting string, so it is necessary to loop through the entire string. On every iteration, we remove an occurance of that letter and check if the letter has been used already. If it in use then there is no need to finish the iteration. However, if the letter is new, then we need to look at the last character in our answer and see if our current character should take its spot. This is done by checking if the last character of the answer is greater than the current character and if there are anymore copies of that last character left in the string (checked through occurance).

At the end of it all, join the array into a string and return

## Example

Assume the following `s`

- _For my sanity, assume the letters in `used` are True else False_

```
s=bcab    ans=[]    occur={'b': 2,'c': 2,'a': 1}    used=[]
```

Start at the beginning of `s` and work way down

```
s=bcab    ans=[b]    occur={'b': 1,'c': 1,'a': 1}    used=[]
s=bcab    ans=[b, c]    occur={'b': 1,'c': 1,'a': 1}    used=[]
```

Now we come across `a` which is smaller than `c` and if `c` was to be removed, there are more opportunities later to add it

```
s=bcab    ans=[b]    occur={'b': 1,'c': 1,'a': 0}    used=[]
```

After `c` is removed, we check if `a` is smaller than `b` which it is and we remove it

```
s=bcab    ans=[]    occur={'b': 1,'c': 1,'a': 0}    used=[]
```

Now there is nothing to comapare to so `a` us added

```
s=bcab    ans=[a]    occur={'b': 1,'c': 1,'a': 0}    used=[]
```

This process goes on until all elements are read

## Code

```python
class Solution:
    def smallestSubsequence(self, s: str) -> str:
        ans = []
        used = [False for _ in len(26)]
        occur = {}
        for c in s:
            occur[c] = occur.get(c, 0) + 1

        for c in s:
            occur[c] -= 1
            if used[ord(c) - ord('a')]:
                continue
            while ans and ans[-1] < c and occur[ans[-1]] > 0:
                used[ord(c) - ord('a')] = True
                ans.pop()
            ans.append(c)
            used[ord(c) - ord('a')] = False

        return "".join(ans)
```
