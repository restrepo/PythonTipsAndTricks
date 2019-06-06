## Include Unicode charactes in word
```python
re.search('\w',s,re.UNIDECODE)
```
## What is the difference between `.*?`  and `.*` regular expressions?
USe: `.*?`, see: https://stackoverflow.com/a/3075150/2268280
## In regex, match either the end of the string or a specific character
See: https://stackoverflow.com/a/12083343/2268280
```python
s1='a;b'
s2='a'
re.search('.*?(;|$)',s1)
```
