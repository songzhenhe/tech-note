# Pandas

This document is for tips using pandas


## pd.read_csv


To keep the first row 0 (as the header) and then skip everything else up to row 10, you can write:
```
pd.read_csv('test.csv', sep='|', skiprows=range(1, 10))
```

Read all lines as values (no header, defaults to integers)
```
pd.read_csv(f, header=None)
```


Use a particular row as the header (skip all lines before that):
```
pd.read_csv(f, header=3)
```

Use a multiple rows as the header creating a MultiIndex (skip all lines before the last specified header line):
```
pd.read_csv(f, header=[2, 4]
```

Skip N rows from the start of the file (the first row that's not skipped is the header):
```
pd.read_csv(f, skiprows=3)   
```

Skip one or more rows by giving the row indices (the first row that's not skipped is the header):
```
pd.read_csv(f, skiprows=[2, 4])  
```

