# 516 Longest Palindromic Subsequence

**Medium**

Given a string `s`, find the longest palindromic subsequence's length in `s`.

## Concept

The idea is to use a 2D DP array where each cell `dp[i][j]` represents the longest palindrome sequence of the string `s[i:j+1]`. By iterating through every substrings of `s`, we check if `s[i]` and `s[j]` are equal. If that is the case, then it is possible to have a palidrome of at least length 1 (2 if we are checking an even substring). If there is room to expand left and right, then we check tack on the possible palindromes of the substring generated. If `s[i]` and `s[j]` do not equate, then we either exclude `s[i]` or `s[j]`, whcih can be done by finding out which one will give us the max value.

## Code

```python
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:

        dp = [[0] * (len(s) + 1) for _ in range(len(s))]

        # Double for loop to try all substrings of s
        for i in range(len(s)):
            for j in range(len(s)-1, i-1, -1):

                # If s[i] and s[j] are the same then we haev a least a palindrome of 1 or 2
                if s[i] == s[j]:
                    dp[i][j] = 1 if i == j else 2
                    # If there is room to expand, add on the palindromes of the substring that happens after the expansion
                    if i - 1 >= 0:
                        dp[i][j] += dp[i-1][j+1]
                else:
                    # Set the number of palindromes to be the length if we skipped the left i
                    dp[i][j] = dp[i][j+1]
                    if i - 1 >= 0:
                        # Set the number of palindromes possible to be the max of either we exclude left or right
                        dp[i][j] = max(dp[i][j], dp[i-1][j])
                res = max(res, dp[i][j])
        return res
```
