# Extract countries from text
Use
```python
pip install geotext
```
Then
```python
from geotext import GeoText
GeoText('Maybe this way: Viet Nam, or this other way: Vietnam'  ).countries
Out[]: ['Vietnam']
```
Add country alias to existing two-letter code (or extra country with new two-letter code)
```python
GeoText.index[2]['viet nam']='VI'
GeoText('Maybe this way: Viet Nam, or this other way: Vietnam'  ).countries
Out[]: ['Viet Nam', 'Vietnam']
```
