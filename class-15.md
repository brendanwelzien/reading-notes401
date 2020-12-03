# Python Regular Expressions
- sequence of characters used to check whether a pattern exists in a given text or string
- used on the server side to validate foramt of addresses or passwords

1. import by use `re`
    a. useful functions --> `compile()`, `search()`, `findall()`, `sub()`, `split()`
## Greedy vs Non-Greedy Matching
- when a special character matches as much of ther search sequence string, it is said to be a greedy match
    - using the `?` modifier makes it perform the same match but in *minimal fashion*

## Summary Table
Character | Functionality
-----|-----
. | a period, matches any single character except newline character
^ | a caret, matches a pattern at the start of the string
\A | Uppercase A, matches only at start of the string
$ | Matches the end of the string
\Z | Matches only at the end of the string
[] | Matches the set of characters you specify within it
\ | if the character following the backslash is an escape character, then the meaning is taken
\ | else the backslash () is treated like any other character and passed through
\ | used in front of all metacharacters to remove special meaning
\w | matches any single letter, digit, or underscore
\W | matches any character not part of \w
\s | matches a single whitespace character like space, newline, tab, return
\S | matches any character not part of \s
\d | matches decimal digit 0-9
\D | matches any character that is not a decimal digit
\t | matches tab
\n | matches newline
\r | matches return
\b | matches only the beginning or end of the word
`+` | checks if preceding character appears one or more times
`*` | checks if preceding character appears zero or more times
? | checks if preceding character appears exactly zero or one time, specifies non greedy version of + and *
{} | checks for explicit number of times
() | creates a group when performing matches
<> | creates a named group when performing matches

## Shutil --> High-level file operations

1. import shutil
-> copyfile() copies contents of source to destination
-> copyfileobj() is a lower level function of copyfile()
-> copy() function interpretes output name
-> copytree() to copy a directory from one place to another, use this
-> which() function finds a search path for a named file

[<-- Back](README.md)