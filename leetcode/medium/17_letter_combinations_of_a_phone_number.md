# 17 Letter Combinations of a Phone Number

**Medium**

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

## Concept

It's just the brute force methode.

Create a conversion table, go through each element of `digits` and add on characters to each element of a list that contains the combination of characters from the previous digits.

## Example

Assume the following `digits`

```
digits="23"     out=[]
```

Start with the first digit in `digits`

```
digits="23"     out=["a", "b", "c"]
```

Move on to the second digit and add each letter of the conversion the each element in `out`

```
digits="23"     out=["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

## Code

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:

        if len(digits) == 0:
            return []

        conversions = {
            "2": "abc",
            "3": "def",
            "4": "ghi",
            "5": "jkl",
            "6": "mno",
            "7": "pqrs",
            "8": "tuv",
            "9": "wxyz"
        }

        res = [""]
        for digit in digits:
            tmp = []
            for prev in res:
                for letter in conversions[digit]:
                    tmp.append(prev + letter)
            res = tmp
        return res
```
