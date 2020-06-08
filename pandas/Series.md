### Series (`ps`)
## REGEX
#### REGEX search and replacement
```python
ps.str.contains(REGEX).str.replace(r'...(REGEX)...',r'...\1...')
```
## `apply` method
#### `apply` template
for a list of dictionaries
```python
pd.apply( lambda l: [d if d else d for d in x] if l else l)
```
* Rebuild a list of dictionaries changing some key
```python
def change_key(l):
    ll=[]
    for d in l:
        d['new']=1
        ll.append(d)
     return ll
pd.apply( lambda l: change_key(l) if l else l)
```
*  Update a dictionary in a list of dictionaries
```python
pd.apply( lambda l: [d.update({'new':1}) for d in x] if l else l)
```

#### Series: Obtain the values of a key in a column of dictionaries:
```python
ps.dict_column.apply(lambda x: x.get('key'))
```
Before some sanity check need to be done.
Either [replace all `NaN` values in the Series with empty python dict objects](https://stackoverflow.com/a/25901013/2268280)
```python
>>> ps=df.R(lambda x: {} if pd.isnull(x) else x)
>>> frame
                    Q          R
0           {2: 2010}  {1: 2013}
1  {2: 2011, 3: 2009}         {}
```
Or by filter out the `NaN` values
```python
(ps[~ps.dict_column.isna()]).dict_column.apply(lambda x: x.get('key'))
```
#### Filter and combain dictionary values from a Series con a list of dictionaries with the same keys.
```python
ps.apply(lambda x: [ str( d.get('key1'))+' '+str(d.get('key2')) for d  in x] )
```

#### How to apply a function to two columns of Pandas dataframe
See also [stackoverflow](http://stackoverflow.com/questions/13331698/how-to-apply-a-function-to-two-columns-of-pandas-dataframe)
```python
kk['lvr']=kk['SO'].str.lower().str.strip().map(un.unidecode).combine(\
  kk['SJR_Title'].str.lower().str.strip().map(un.unidecode) , func=lv.ratio)
```

#### Flatten column with lists of lists into a single list:
See: https://stackoverflow.com/a/38896038/2268280
```
df['col'].apply(pd.Series).stack().unique()
```

### Recommended way to update key in a list of dictionaries
```python
def func(l):
    for i in range(len(l)):
        l[i].get('key')='NEW VALUE'
     ...
     return l
>>> df['col'].apply(func)
```

## Other
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

#### Select the first two words from a colum text
```python
s=' '.join(ext.UDEA_título.str.lower().str.replace(' ',':: ').str.split('::').str[:2].loc[i])
```
#### map  upon series with a parameter
```python
ps.map(lambda x: lv.ratio(x,parameter))
```
#### Plot histrogram
```python
ps.value_counts().plot(kind='bar')
```
Sorting index
```python
ps.value_counts().sort_index().plot(kind='bar')
```
or values
```python
ps.value_counts().sort_values().plot(kind='bar')
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


### Advanced examples
#### `lambda` function to combine two columns with conditonal in both columns
Normalize a column with `NaN` to string `date` format 'YYYY-MM-DD' from a column with integer `year`:
```python
df.date.combine(df.year,func=lambda x,y: y if y>-1 and pd.isnull(x) else x)
```

