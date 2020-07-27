## HTTP server
```python
$ python -m http.server 8001
```
## Convert variable names to string
See https://stackoverflow.com/a/61994365/2268280
```python
>>> def tostr(**kwargs):
    return kwargs

>>> var = {}
>>> something_else = 3
>>> tostr(var = var,something_else=something_else)
{'var' = {},'something_else'=3}
```
## Specific modules
### Language tools
See: https://www.geeksforgeeks.org/detect-an-unknown-language-using-python/ for suggested modules
* `pip install langdetect`
* `pip install textblob`
* `pip install langrid`
With `textblob`
```python
from textblob import TextBlob 
TextBlob('On a minimal factorization conjecture').detect_language()
[Out]: en
```
