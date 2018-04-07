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
#### Select the first two words from a colum text
```python
s=' '.join(ext.UDEA_título.str.lower().str.replace(' ',':: ').str.split('::').str[:2].loc[i])
```
#### map  upon series with a parameter
```python
ps.map(lambda x: lv.ratio(x,parameter))</code>
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

### Calculates the maximum between columns
See [here](https://stackoverflow.com/a/20033232)
```python
frame[['test1','test2','test3']].max(axis=1)
```
