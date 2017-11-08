### Series (`ps`)
#### REGEX search and replacement
<code>ps.str.contains(REGEX).str.replace(r'...(REGEX)...',r'...\1...')</code>
#### Change type
For example for `str` to something else

```ps.str.replace('^$','0').astype(TYPE)</code>```

with type: `float, int,...`
#### Series: Obtain first value of a list after `str.split(pattern)`
<code>ps.título.str.lower().map(unidecode).str.split('(').str[0]</code>
#### Select the first two words from a colum text
<code> s=' '.join(ext.UDEA_título.str.lower().str.replace(' ',':: ').str.split('::').str[:2].loc[i])</code>
#### map  upon series with a parameter
<code>ps.map(lambda x: lv.ratio(x,parameter))</code>
#### How to apply a function to two columns of Pandas dataframe
See also [stackoverflow](http://stackoverflow.com/questions/13331698/how-to-apply-a-function-to-two-columns-of-pandas-dataframe)
```python
kk['lvr']=kk['SO'].str.lower().str.strip().map(un.unidecode).combine(\
  kk['SJR_Title'].str.lower().str.strip().map(un.unidecode) , func=lv.ratio)
```
#### Apply method with condition
```python
applymap(lambda x: x.encode('unicode_escape').
                 decode('utf-8') if isinstance(x, str) else x).to_excel('kk.xlsx')
```
#### Plot histrogram
```python
ps.value_counts().plot(kind='bar')
```
<img src='year.png'>
