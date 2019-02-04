### Series (`ps`)
#### REGEX search and replacement
```python
ps.str.contains(REGEX).str.replace(r'...(REGEX)...',r'...\1...')
```

#### Change type
For example for `str` to something else

```python
ps.str.replace('^$','0').astype(TYPE)
```

with type: `float, int,...`

#### Series: Obtain first value of a list after `str.split(pattern)`
```python
ps.título.str.lower().map(unidecode).str.split('(').str[0]
```

#### Series: Obtain the values of a key in a column of dictionaries:
```python
ps.dict_column.apply(lambda x: x.get('key'))
```

#### Select the first two words from a colum text
```python
s=' '.join(ext.UDEA_título.str.lower().str.replace(' ',':: ').str.split('::').str[:2].loc[i])
```
#### map  upon series with a parameter
```python
ps.map(lambda x: lv.ratio(x,parameter))
```
#### How to apply a function to two columns of Pandas dataframe
See also [stackoverflow](http://stackoverflow.com/questions/13331698/how-to-apply-a-function-to-two-columns-of-pandas-dataframe)
```python
kk['lvr']=kk['SO'].str.lower().str.strip().map(un.unidecode).combine(\
  kk['SJR_Title'].str.lower().str.strip().map(un.unidecode) , func=lv.ratio)
```
#### Plot histrogram
```python
ps.value_counts().plot(kind='bar')
```

#### Convert two series of numbers into a series of the list of numbers
```python
ps['col1'].map( lambda x: [x] )+ps['col1'].map( lambda x: [x] )
```

#### Convert a list of integers into a list of strings and join them with separator
```python
ps['col_list'].map( lambda x: 
                            '\n'.join(  
                                list( map(str, x) ) 
                                  ) 
                            )
```
#### Obtain elements by slice
```python
ps.iloc[1:7]
```

#### Fill missing keys from a list with empty string
```python
def add_blank_missing_keys(ps,keys):
    '''
    Check if the keys are in a Pandas Series.
    If not the key value is initialized with
    the empty string
    '''
    for k in keys:
        ps[k]=ps.get(k)
    #Replace None with empty string
    return ps.fillna('')    
```

#### Column with list into a single list:
See: https://stackoverflow.com/a/38896038/2268280
```
df['col'].apply(pd.Series).stack().tolist()
```
