# 49 Group Anagrams

**Medium**

Given an array of strings `strs`, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Concept

Anagrams will be grouped together through a hashtable. The `key` indicates the features that determine if a word belongs in that anagram or `value` which is a list. Keys can vary an array indicating occurance of each letter in a word, the sorted version of the word, and the sum of all the word's characters ascii value. Go through the list of strings and organize the words in the hash table accordingly.

## Example

Start with a fresh map and begin iterating through the strings

```
strs = ["eat","tea","tan","ate","nat","bat"]    angarams = {}
```

In this example the words are grouped by the sorted order of the words characters since only angrams will result in the same ordered characters string

```
current = "eat"     anagrams = {}
current = "tea"     anagrams = {"aet": ["eat"]}
current = "tan"     anagrams = {"aet": ["eat", tea]}
current = "ate"     anagrams = {"aet": ["eat", tea], "ant": ["tan"]}
...
```

## Code

**Using sorted characters** (like example)

```python
def groupAnagrams(self, strs: List[str]) -> List[List[str]]:

    def sortString(word):
        wordList = list(word)
        return "".join(sorted(wordList))

    anagrams = {}
    for word in strs:
        sortedWord = sortString(word)
        if sortedWord in anagrams:
            anagrams[sortedWord].append(word)
        else:
            anagrams[sortedWord] = [word]

    return list(anagrams.values())
```

**Using string value**

```python
def groupAnagrams(self, strs: List[str]) -> List[List[str]]:

    def wordValue(word):
        val = 0
        for c in word:
            val += ord(c)
        return val

    anagrams = {}
    for word in strs:
        wordVal = wordValue(word)
        if wordVal in anagrams:
            anagrams[wordVal].append(word)
        else:
            anagrams[wordVal] = [word]

    return list(anagrams.values())
```
