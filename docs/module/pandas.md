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








The iloc indexer syntax is data.iloc[<row selection>, <column selection>], which is sure to be a source of confusion for R users. 
“iloc” in pandas is used to select rows and columns by number, in the order that they appear in the data frame. 
You can imagine that each row has a row number from 0 to the total rows (data.shape[0])  and iloc[] allows selections based on these numbers. 
The same applies for columns (ranging from 0 to data.shape[1] )


# Single selections using iloc and DataFrame
# Rows:
data.iloc[0] # first row of data frame (Aleshia Tomkiewicz) - Note a Series data type output.
data.iloc[1] # second row of data frame (Evan Zigomalas)
data.iloc[-1] # last row of data frame (Mi Richan)
# Columns:
data.iloc[:,0] # first column of data frame (first_name)
data.iloc[:,1] # second column of data frame (last_name)
data.iloc[:,-1] # last column of data frame (id)


# Multiple row and column selections using iloc and DataFrame
data.iloc[0:5] # first five rows of dataframe
data.iloc[:, 0:2] # first two columns of data frame with all rows
data.iloc[[0,3,6,24], [0,5,6]] # 1st, 4th, 7th, 25th row + 1st 6th 7th columns.
data.iloc[0:5, 5:8] # first 5 rows and 5th, 6th, 7th columns of data frame (county -> phone1).






pandas.unique
pandas.drop

read into one dataframe
df_allraw =  pd.concat(pd.read_excel("cpt.xls", sheet_name=None), ignore_index=True)

read in as dictionary
allraw = pd.read_excel("cpt.xls", sheet_name=None)


import pandas as pd
all_dfs = pd.read_excel(workbook_url, sheet_name=None)
all_dfs.keys()
all_dfs['Sheet1'].head()



list(newdict.keys()).
