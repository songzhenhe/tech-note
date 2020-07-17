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

