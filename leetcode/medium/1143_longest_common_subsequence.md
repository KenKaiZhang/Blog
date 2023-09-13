# 1143 Longest Common Subsequence

**Medium**

Given two strings `text1` and `text2`, return the length of their longest common subsequence. If there is no common subsequence, return 0.

## Concept

This is a 2D dynamic programming problem.

The 2D matrix represents the comparison between `text1` from index row and `text2` from index column. The process should start from the bottom right of the matrix and work up to the top left. Along the way there will be two conditions:

1. If `text1[row] == text2[column]` then `dp[row][column]` will be set to `1 + dp[row][column]`, basically 1 + the value stored in the diagonal since diagonal movement means a match
2. If `text1[row] != text2[column]` then `dp[row][column]` will be the max value of the right or bottom cells since moving horizontally/vertically means skipping a character

At the end, the answer will be in the top left cell.

Watch [NeetCode's solution](https://www.youtube.com/watch?v=Ua0GhsJSlWM) for a better understanding

## Code

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        dp = [[0 for _ in range(len(text1)+1)] for _ in range(len(text2)+1)]

        for i in range(len(text1)):
            for j in range(len(text2)):
                if text1[i] == text2[j]:
                    dp[i][j] = 1 + dp[i+1][j+1]
                else:
                    dp[i][j] = max(dp[i+1][j], dp[i][j+1])
        return dp[0][0]
```
