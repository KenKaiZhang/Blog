# 647 Palindromic Substrings

**Medium**

Given a string `s`, return the number of palindromic substrings in it.

## Concept

The simple way would be to create palindrome with each character as the center and see if that palindrome has been made before. If it has, then don't increment `res`, otherwise increment it.

The more creative approach is to realize the pattern between the length of the string to the number of palindrome it will contain:

- Palindromes with length of 1 and 2 will contain 1 palindrome
  - `"a"` and `"aa"` both contain 1 unique palindrome
- Palindromes with length 2 and 4 will contain 2 palindromes
  - `"aba"` and `abba` will contains the string itself and the individuals (odd and even) in it
- And the this patterns continues

Knowing this pattern allows us to realize that by getting the length of the current palindrome and then dividing it b 2 will result in the number of new palindromes found.

## Code

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        res = 0
        N = len(str)

        for i in range(N):
            # Basically odd and even centers
            for a,b in [[i,i], [i,i+1]]:
                while 0 <= a and b < N and s[a] == s[b]:
                    a -= 1
                    b += 1
                res += (b-a) // 2
        return res
```
