# File Handling


## Ignore Rows

skip header row

``` python
with open(fname) as f:
    next(f)
    for line in f:
        #do something
```

ignore blank lines

``` python
def nonblank_lines(f):
    for l in f:
        line = l.rstrip()
        if line:
            yield line

with open(filename) as f_in:
    for line in nonblank_lines(f_in):
        # Stuff
```

