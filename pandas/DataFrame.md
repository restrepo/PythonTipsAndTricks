# Pandas DataFrame (`df`)

## Miscellaneous
### Configuration
```python
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.max_colwidth',200)
```

### Show specific file
```python
    df.loc[[223,415]]
```


## `apply`
### `apply` in column
### `apply` method with condition
```python
df=pd.DataFrame({'A':['a',2]}).applymap(lambda x:x-1 if isinstance(x,int) else x)
print(df)
   A
0  a
1  1
```
### Filter in a column with a list a dictionary by dictionary key
```python
df[ df['column'].apply(lambda l: [d.get('key')==value for d in l] 
       if l else [False]).apply(lambda l: True in l) ]
```
### `apply` in row
### Use `apply` in multiple columns of a DataFrame with `axis=1`
Based on https://stackoverflow.com/a/16354730
General help:
```python
df.apply(lambda row: row['a'] % row['c'],axis=1)
```
Details...
```python
def my_test2(row):
    return row['a'] % row['c']
df = DataFrame ({'a' : np.random.randn(6),
                 'b' : ['foo', 'bar'] * 3,
                 'c' : np.random.randn(6)})

df['Value'] = df.apply(lambda row: my_test(row['a'], row['c']), axis=1)
df
Out[..]:
                    a    b         c     Value
          0 -1.674308  foo  0.343801  0.044698
                       ...
```
To apply in all entries use `df.applymap`

It can be used to merge two columns
```python
df.apply(lambda row: row['A'] if row['A'] else row['B'],axis=1 )
```
### Recommended way to update key in a list of dictionaries
```python
def func(row):
    for i in range(len(row['col'])):
        row['col'][i].get('key')='NEW VALUE'
     ...
     return row['col']
>>> df['col'].apply(func,axis='columns')
```

### `apply` in full DataFrame
* Apply a function to a Dataframe elementwise.
```python
df.applymap(func)
```

## Tips & Tricks
### Drop duplicates:
```python
    df.drop_duplicates(subset=['column_name']).reset_index(drop=True)
```
### False positive in `df.loc[row_index,col_indexer]`
```python
pd.options.mode.chained_assignment = None  # default='warn'
```
### drop colums with `NaN` entries
```python
df.drop(['col_1','col_2'],axis='columns')
```
### drop colums
```python
df.dropna(axis=1)
```
### Drop DF entries from a list of indices:
`mi` is the list of indices
```python
df.drop(df.index[list(mi)]
```
### `df1` DataFrame with `df2` indexes
```python
if df1.shape[0]==df2.shape[0]: # df1.index!=df2.index
   df1.index=df2.index.values
```
### Rename columns of DF
```python
df.rename({'OLD':'NEW'}, axis = 'columns')
```
### Rename index of DF
```python
    df.rename(index={0:'hello',1:'world'})
```
### Check duplicates of a df
```python
df[df.duplicated()]
```
or
```
df[df.duplicated('column')]
```
### Changing columns inside function: pass always as `df.copy()`
If a df is passed as a function argument, a column change could propagate outsided the function. To avoid problems
pass a hard copy of the df to the function through `df.copy()`
### Drop duplicate entries after manipulations
```python
df_all=df[df.duplicated('KEY',keep=False)]
df_unique=df.drop_duplicates('KEY')]
for i in df_unique.index:
    mtch=df[df['KEY']==df_all.loc[i,'KEY']
    if mctch.shape[0]:
       .....
```
### Combine two Pandas dataframes with the same index
```python
pandas.concat([df1, df2], axis=1)
```
### df  query
```python
from numpy.random import randn
from pandas import DataFrame
df = DataFrame(randn(10, 2), columns=list('ab'))
df.query('a > b')
df[df.a > df.b]  # same result as the previous expression
```
### Merge
```python
import pandas as pd
l=pd.DataFrame()
l=l.append(pd.Series({'T':'A','W':10}),ignore_index=True)
l=l.append(pd.Series({'T':'B','W':1}),ignore_index=True)
r=pd.DataFrame()
r=r.append(pd.Series({'T':'A','S':2}),ignore_index=True)
r=r.append(pd.Series({'T':'C','S':1}),ignore_index=True)
print(l.merge(r,on='T',how='outer').fillna(0))
print('='*15)
print(l.merge(r,on='T',how='left').fillna(0))
print('='*15)
print(l.merge(r,on='T',how='right').fillna(0))
print('='*15)
print(l.merge(r,on='T',how='inner').fillna(0))
   T     W    S
0  A  10.0  2.0
1  B   1.0  0.0
2  C   0.0  1.0
===============
   T     W    S
0  A  10.0  2.0
1  B   1.0  0.0
===============
   T     W    S
0  A  10.0  2.0
1  C   0.0  1.0
===============
   T     W    S
0  A  10.0  2.0
```
### Creates df on flight
```python
pd=pd.DataFrame()
pd.loc[10,'hello']='world'
```

### Calculates the maximum between columns
See [stackoverflow](https://stackoverflow.com/a/20033232)
```python
df[['test1','test2','test3']].max(axis=1)
```

### Write text file with quoted text even for single words
```python
import csv
df.to_csv('file.csv',sep=' ',
           quoting=csv.QUOTE_NONNUMERIC,header=False,index=False)
```

### Combine two columns of text in dataframe
See also [here](https://stackoverflow.com/a/19378497/2268280)
```python
df['FULL NAME']=df['NAME']+' '+df['SURNAME']
```
### [Drop rows of a DataFrame based in a specific list of values o some column](https://stackoverflow.com/a/27965386/2268280), e.g `'datecolumn'`
```python
df = df[~df.datecolumn.isin(a)]
```

### Count elements of a DataFrame `column`,for example: `dptos`
```python
df.groupby('dptos')['dptos'].count().sort_values(ascending=False)
dptos
Instituto de Física                                             862
Instituto de Biología                                           656
Instituto de Química                                            645
Departamento de Matemáticas                                     130
```

### Logical filters in DataFrame`
```python
#For AND
df[ ( df['col1']>0 ) & df['col2']<10 ) ]
# For OR use `|`
```
### Replacing NaN with None in Pandas DataFrame or Series
See: https://stackoverflow.com/a/14163209/2268280
```python
df=df.where((pd.notnull(df)), None)
```
### Convert Data Frame to a list of dictionaries
```python
df.to_dict('records')
```

### Insert list into a cell
See https://stackoverflow.com/a/47548471/2268280
```python
df['B'] = df['B'].astype('object')
df.at[1, 'B'] = [1, 2, 3]
```

### Mask based in contained string with `NaN` in columns
```python
df[df.str.contains('query',na=False)]
```


## Input/Output
### Write/read full objects 
Used `hdf` which allow to save several dataframes to the same file:
```python
df.to_hdf('file.hdf5','FreeKey')
```


## Read data

### CSV

#### Read pandas data frame with column objects from csv (or excel) file
When the objects are complex numbers or `numpy arrays`:
```python
import pandas as pd
import numpy as np
def read_csv_objects(file,columns,**kwargs):
    '''
    Read pandas data frame with column objects from csv (or excel) file
    columns is the column or list of columns which contains the objects,
    ''' 
    df=pd.read_csv(file,**kwargs)
    columns=list(columns)
    for c in columns:
        df[c]=df[c].str.replace('\n',',').apply(lambda x: eval(x)  )
        if df[c].dtype == list:
            df[c]=df[c].apply(lambda x: np.array(x))
        
    return df
```    

#### Read a long csv file
Use `low_memory=False`. For example [here](https://www.kaggle.com/diegorestrepo/kernel1f8af0b449)
```python
cv=pd.read_csv('/kaggle/input/CORD-19-research-challenge/metadata.csv',low_memory=False)
```

### JSON
#### Read line-delimited "JSON-lines" data
```bash
$ cat kk.json
{"A":1,"B":3}
{"A":5,"B":6}
```
Read with the following options:
```python
pd.read_json('kk.json',orient='records',lines=True)
```

#### Read a json dictionary
Udea `orient='index'`. See for example [here](https://www.kaggle.com/diegorestrepo/kernel1f8af0b449)
```python
a=pd.read_json(url, orient='index').T
```
#### Fix integer key in column of dictionaries when load from JSON
Wrongly load as
```python
>>> df.loc[0,'d']
{'1':'A'}
```
See https://stackoverflow.com/a/34346202/2268280
```python
def jsonKeys2int(x):
    if isinstance(x, dict):
            return {int(k):v for k,v in x.items()}
    return x
>>> df['d']=df['d'].apply(jsonKeys2int)
>>> df.loc[0,'d']
{1:'A'}
```

## Write data
### JSON
#### Write to json by using the standard format that can be read also with `json.loads`
Also to enforce UTF-8 encoding and properly characters like 'π' whithout escaping
```python
df.to_json('file.json',orient='records',force_ascii=False)
```
#### Read the JSON data
This can be read either as
```python
pd.read_json('file.json')
```
or Directly a full json list of dictionaries
* Full file
```python
with open(r"file.json", "r") as read_file:
    data = json.load(read_file)
```
* For a compressed json with UTF-8 encoding (see: https://stackoverflow.com/a/39451012/2268280):
```python
import gzip
with gzip.GzipFile('file.json.gz', 'r') as read_file:
    data = json.loads(read_file.read().decode('utf-8'))
```
* Line by line to avoid encoding problems (see: https://stackoverflow.com/a/29312618/2268280)
```python
data = []
for line in open('file.json', 'r'):
    data.append(json.loads(line))
```
