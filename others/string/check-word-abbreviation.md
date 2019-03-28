Check Word Abbreviation 解题报告

Given a**non-empty**string`word`and an abbreviation`abbr`, return whether the string matches with the given abbreviation.

A string such as`"word"`contains only the following valid abbreviations:

```
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]

```

##### Notice

Notice that only the above abbreviations are valid abbreviations of the string`word`. Any other string is not a valid abbreviation of`word`.

  
**Example**

Example 1:

```
Given s = "internationalization", abbr = "i12iz4n":
Return true.

```

Example 2:

```
Given s = "apple", abbr = "a2e":
Return false.

```

```
class Solution:
    """
    @param: word: a non-empty string
    @param: abbr: an abbreviation
    @return: true if string matches with the given abbr or false
    """
    def validWordAbbreviation(self, word, abbr):
        # write your code here
        i, j = 0, 0
        while i < len(word) and j < len(abbr):
            if abbr[j].isdigit():
                if abbr[j] == '0':
                    return False
                length = 0
                while j < len(abbr) and abbr[j].isdigit():
                    length = length * 10 + int(abbr[j])
                    j += 1
                i += length
            else:
                if word[i] != abbr[j]:
                    return False
                i += 1
                j += 1
        return i == len(word) and j == len(abbr)

```



