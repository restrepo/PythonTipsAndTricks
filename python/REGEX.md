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
## Apply a method to the selected group
or Calling a function on captured group in re.sub()

Example: Title string only in long words
```python
>>> s='Facultad de ciencias exactas y naturales'
>>> re.sub('(\s[A-Za-z]{1,3}\s)',lambda m: m.group(0).lower(),s.title(),re.UNICODE)
'Facultad de Ciencias Exactas y Naturales'
```

Example: Fix BibTex:
See https://stackoverflow.com/a/17136150/2268280
```python
from unidecode import unidecode
re.sub(r'\\(.)',
       lambda m: 'í'+unidecode(m.group(1)),
       'Ram\\ŕez-V\\ĺlareal, Álvaro and Restrepo, Diego')
```
→ `Ramírez-Víllareal, Álvaro and Restrepo, Diego`
