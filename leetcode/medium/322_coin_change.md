# 322 Coin Change

**Medium**

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

## Concept

This is a dp problem.

Find minimum possible combination of coins form 0 -> `amount` by checking each coin value, seeing the max number of said coin usable in the amount and then if there are any remainders, go find it in the dp since it's going to be less than the current amount and has been calculated before.

## Example

Assume the given

- dp will be size of amount + 1 since we include 0 and 0 can be set to 0 (duh)

```
coins = [1,2,5]     amount = 11     dp = [0,12,12, ... ,12]
```

Start at sub amount 1. The minimum number of coins need to make 1 is 1 using 1 since 2 and 5 are too big.

```
sub = 1     dp = [0,1,12, ... ,12]
```

2 follows the same concept

```
sub = 2    dp = [0,1,1, ... ,12]
```

3 will have 1 and 2 checked where if we only used 1 the `dp[3]` would be 3. However when 2 is tried, we will have a remainder of 1, meaning `dp[3]` will be 1 (since 1 2 coin fits in 3) and however many coins it takes to make up the value 1 (which can be found in `dp[1]`)

```
sub = 3     dp = [0,1,1,2, ... ,12]
```

Continue this process until the end of dp. If dp ends up not being the default value (which we set to `amount` + 1 since if `coins` only consist of 1, then its impossible to hit the default)

## Code

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [amount + 1 for _ in range(amount)]
        dp[0] = 0

        for sub in range(1, amount+1):
            for c in coins:
                able = sub // c
                if able > 0:
                    dp[sub] = min(dp[sub], able + dp[sub - (able * c)])
        return dp[-1] if dp[-1] != amount + 1 else -1
```
