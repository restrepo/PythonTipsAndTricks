## Include Unicode characters in word
```python
re.search('\w',s,re.UNIDECODE)
```
## What is the difference between `.*?`  and `.*` regular expressions?
Use: `.*?`, see: https://stackoverflow.com/a/3075150/2268280
## In regex, match either the end of the string or a specific character
See: https://stackoverflow.com/a/12083343/2268280
```python
s1='a;b'
s2='a'
re.search('.*?(;|$)',s1)
```
## Replace lowercase letter for uppercase
```python
ss=Mcewen
re.sub( 'Mc(\w)',lambda s: 'Mc'+s.group(1).upper(),ss)
McWewen
```
## Match start or whitespace
Also works for end or whitespace:

`\b` is word boundary, which can be a white space, the beginning of a line or a non-alphanumeric symbol
