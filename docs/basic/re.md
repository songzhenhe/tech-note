# RegEx

[`RegEx`](https://docs.python.org/3/howto/regex.html) : regular expressions 
in Python with the [`re`](https://docs.python.org/3/library/re.html#module-re "re: Regular expression operations.") module


## RegEx Functions

| Function | Description                                                       |
|----------|-------------------------------------------------------------------|
| findall  | Returns a list containing all matches                             |
| search   | Returns a Match object if there is a match anywhere in the string |
| split    | Returns a list where the string has been split at each match      |
| sub      | Replaces one or many matches with a string                        |



## Metacharacters


| Character | Description                                                                  | Example        |
|-----------|------------------------------------------------------------------------------|----------------|
| []        | A set of characters                                                          | "[a-m]"        |
| \         | Signals a special sequence (can also be used to escape special   characters) | "\d"           |
| .         | Any character (except newline character)                                     | "he..o"        |
| ^         | Starts with                                                                  | "^hello"       |
| $         | Ends with                                                                    | "world$"       |
| *         | Zero or more occurrences                                                     | "aix*"         |
| +         | One or more occurrences                                                      | "aix+"         |
| {}        | Exactly the specified number of occurrences                                  | "al{2}"        |
| \|        | Either or                                                                    | "falls\|stays" |
| ()        | Capture and group                                                            |                |


The findall() function returns a list containing all matches.  

``` python
import re

txt = "The rain in Spain"
x = re.findall("ai", txt)
print(x)
```
