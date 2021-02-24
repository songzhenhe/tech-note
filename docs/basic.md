[toc]

# Python Data Types

* Text Type:  str
* Numeric Types:  int, float, complex
* Sequence Types:  list, tuple, range
* Mapping Type:  dict
* Set Types:  set, frozenset
* Boolean Type:  bool
* Binary Types:  bytes, bytearray, memoryview



| Example                                      | Data Type  |
|----------------------------------------------|------------|
| x = "Hello World"                            | str        |
| x = 20                                       | int        |
| x = 20.5                                     | float      |
| x = 1j                                       | complex    |
| x = ["apple", "banana", "cherry"]            | list       |
| x = ("apple", "banana", "cherry")            | tuple      |
| x = range(6)                                 | range      |
| x = {"name" : "John", "age" : 36}            | dict       |
| x = {"apple", "banana", "cherry"}            | set        |
| x = frozenset({"apple", "banana", "cherry"}) | frozenset  |
| x = True                                     | bool       |
| x = b"Hello"                                 | bytes      |
| x = bytearray(5)                             | bytearray  |
| x = memoryview(bytes(5))                     | memoryview |




\n (backslash n)    a new line character

# Build in Function

## zip() Function


``` python
a = ("John", "Charles", "Mike")
b = ("Jenny", "Christy", "Monica", "Vicky")

x = zip(a, b)
```

``` python
name = [ "Manjeet", "Nikhil", "Shambhavi", "Astha" ] 
roll_no = [ 4, 1, 3, 2 ] 
marks = [ 40, 50, 60, 70 ] 
mapped = zip(name, roll_no, marks) 
# converting values to print as set 
mapped = set(mapped) 
# printing resultant values 
print ("The zipped result is : ",end="") 
print (mapped)

# output
The zipped result is : {('Shambhavi', 3, 60), ('Astha', 2, 70),
('Manjeet', 4, 40), ('Nikhil', 1, 50)}
```

``` python
numbers = [1, 2, 3]
letters = ['a', 'b', 'c']
zipped = zip(numbers, letters)
type(zipped)

# output
<class 'zip'>

# zip() function returns an iterator, use list() to consume the iterator
list(zipped)
# output
[(1, 'a'), (2, 'b'), (3, 'c')]
```



# File Handling



## Directory

os.getcwd() function to get the current working directory
os.chdir() function to change the current working directory.
os.path.join() function constructs a pathname out of one or more partial pathnames. 
os.path.expanduser() function will expand a pathname that uses ~ to represent the current user’s home directory. 


### glob

glob module is another tool in the Python standard library

The glob module uses shell-like wildcards.



## File Open


[`open()`](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files) : Reading and Writing Files 

* "r" - Read - Default value. Opens a file for reading, error if the file does not exist
* "a" - Append - Opens a file for appending, creates the file if it does not exist
* "w" - Write - Opens a file for writing, creates the file if it does not exist
* "x" - Create - Creates the specified file, returns an error if the file exists

``` python
f = open('workfile', 'w')
```

Read Only Parts of the File
read()


## Read Files

``` python
f = open("demofile.txt", "r")
print(f.read())
```

### Read Lines

It is a good practice to always close the file when you are done with it.

``` python
f = open("demofile.txt", "r")
print(f.readline())
f.close()
```

## File Write

### Existing File

* "a" - Append - will append to the end of the file
* "w" - Write - will overwrite any existing content

### Create a New File

* "x" - Create - will create a file, returns an error if the file exist
* "a" - Append - will create a file if the specified file does not exist
* "w" - Write - will create a file if the specified file does not exist





seek(0) : Move the read/write location to the beginning of the file.



os.path.basename() and os.path.dirname()?
Both functions use the os.path.split(path) function to split the pathname path into a pair; (head, tail).

The os.path.dirname(path) function returns the head of the path.

E.g.: The dirname of '/foo/bar/item' is '/foo/bar'.

The os.path.basename(path) function returns the tail of the path.

E.g.: The basename of '/foo/bar/item' returns 'item'

# RegEx

[`RegEx`](https://docs.python.org/3/howto/regex.html) : regular expressions 
in Python with the [`re`](https://docs.python.org/3/library/re.html#module-re "re: Regular expression operations.") module


## RegEx Functions

| Function | Description                                                  |
| -------- | ------------------------------------------------------------ |
| findall  | Returns a list containing all matches                        |
| search   | Returns a Match object if there is a match anywhere in the string |
| split    | Returns a list where the string has been split at each match |
| sub      | Replaces one or many matches with a string                   |



## Metacharacters


| Character | Description                                                  | Example        |
| --------- | ------------------------------------------------------------ | -------------- |
| []        | A set of characters                                          | "[a-m]"        |
| \         | Signals a special sequence (can also be used to escape special   characters) | "\d"           |
| .         | Any character (except newline character)                     | "he..o"        |
| ^         | Starts with                                                  | "^hello"       |
| $         | Ends with                                                    | "world$"       |
| *         | Zero or more occurrences                                     | "aix*"         |
| +         | One or more occurrences                                      | "aix+"         |
| {}        | Exactly the specified number of occurrences                  | "al{2}"        |
| \|        | Either or                                                    | "falls\|stays" |
| ()        | Capture and group                                            |                |


The findall() function returns a list containing all matches.  

``` python
import re

txt = "The rain in Spain"
x = re.findall("ai", txt)
print(x)
```