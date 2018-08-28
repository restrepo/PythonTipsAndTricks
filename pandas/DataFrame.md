## Pandas

### Data-Frames (`df`)

##### Configuration
```python
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.max_colwidth',200)
```

##### Show specific file
```python
    df.loc[[223,415]]
```

##### Drop duplicates:
```python
    df.drop_duplicates(subset=['column_name']).reset_index(drop=True)
```
#### False positive in `df.loc[row_index,col_indexer]`
```python
pd.options.mode.chained_assignment = None  # default='warn'
```
#### drop colums
```python
udea.drop(['dict_doi','match'],axis='columns')
```
#### Drop DF entries from a list of indices:
`mi` is the list of indices
```python
df.drop(df.index[list(mi)]
```
#### `df1` DataFrame with `df2` indexes
```python
if df1.shape[0]==df2.shape[0]: # df1.index!=df2.index
   df1.index=df2.index.values
```
#### Rename columns of DF
```python
df.rename({'OLD':'NEW'}, axis = 'columns')
```
#### Rename index of DF
```python
    df.rename(index={0:'hello',1:'world'})
```
#### Check duplicates of a df
```python
df[df.duplicated()]
```
or
```
df[df.duplicated('column')]
```
#### Changing columns inside function: pass always as `df.copy()`
If a df is passed as a function argument, a column change could propagate outsided the function. To avoid problems
pass a hard copy of the df to the function through `df.copy()`
#### Drop duplicate entries after manipulations
```python
df_all=df[df.duplicated('KEY',keep=False)]
df_unique=df.drop_duplicates('KEY')]
for i in df_unique.index:
    mtch=df[df['KEY']==df_all.loc[i,'KEY']
    if mctch.shape[0]:
       .....
```
#### Combine two Pandas dataframes with the same index
```python
pandas.concat([df1, df2], axis=1)
```
#### df  query
```python
from numpy.random import randn
from pandas import DataFrame
df = DataFrame(randn(10, 2), columns=list('ab'))
df.query('a > b')
df[df.a > df.b]  # same result as the previous expression
```
#### Merge
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
#### Creates df on flight
```python
pd=pd.DataFrame()
pd.loc[10,'hello']='world'
```
#### Apply method with condition
```python
df=pd.DataFrame({'A':['a',2]}).applymap(lambda x:x-1 if isinstance(x,int) else x)
print(df)
   A
0  a
1  1
```

#### Calculates the maximum between columns
See [stackoverflow](https://stackoverflow.com/a/20033232)
```python
df[['test1','test2','test3']].max(axis=1)
```

#### Write text file with quoted text even for single words
```python
import csv
df.to_csv('file.csv',sep=' ',
           quoting=csv.QUOTE_NONNUMERIC,header=False,index=False)
```
#### Write/read full objects 
Used `hdf` which allow to save several dataframes to the same file:
```python
df.to_hdf('file.hdf5','FreeKey')
```

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

#### Combine two coluns of text in dataframe
See also [here](https://stackoverflow.com/a/19378497/2268280)
```python
df['NAME']+' '+df['SURNAME']
```
