# Python `Class`

## Special `Class` methods
See:
* https://rszalski.github.io/magicmethods/ [backup](https://web.archive.org/web/20190818113856/https://rszalski.github.io/magicmethods/) 
 
Example
```python
class A:
    def __init__(self):
        self.var='value' #Only defined after instance is created; i=A() -> A.var
    def __call__(self,x):
        return x+1
    def __setitem__(self,k,v):
        '''See: http://www.diveintopython.net/object_oriented_framework/special_class_methods.html'''
        print({k:v})
```

## Add new methods to existing Python object
Example with `list`:
```python
import sys
class list_of_dictionaries(list):
    '''
    Return a dictionary for single results o a list of results
    '''
    def filter(self,k,v,first=False):
        if type(self[0])!=dict:
            sys.exit('NOT A LIST OF DICTIONARIES')
        
        x=[d for d in self if d.get(k)==v]
        if not x:
            x=[{}]
        if first:
            return x[0]
        else:
            return x
```

## Enrich dictionary to use `a['b']` as `a.b`
> The goal is to create a mock class which behaves like a db resultset.

From [here](https://stackoverflow.com/a/1328686/2268280): So what you want is a dictionary where you can spell a['b'] as a.b?

That's easy:

    class atdict(dict):
        __getattr__= dict.__getitem__
        __setattr__= dict.__setitem__
        __delattr__= dict.__delitem__

## `__setitem__` and `__getitem__`
