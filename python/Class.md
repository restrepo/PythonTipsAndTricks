# Python `Class`

## Special `Class` methods
See:
* https://rszalski.github.io/magicmethods/ ([backup](https://web.archive.org/web/20190818113856/https://rszalski.github.io/magicmethods/))
 
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
Discussion about Python `super` https://realpython.com/python-super/ ([Backup][https://web.archive.org/web/20190922043302/https://realpython.com/python-super/] to implement __inheritance__.)

`super()` gives you access to methods in a superclass from the subclass that inherits from it.

`super()` is the same as `super(__class__, <first argument>)`: the first is the subclass, and the second parameter is an object that is an instance of that subclass.

Example with `list`. Be sure that `__add__` return the new object
```python
import sys
class list_of_dictionaries(list):
    '''
    Return a dictionary for single results o a list of results
    '''
    def __add__(self,other):
        return ADD(super(ADD, self).__add__(other))
        #or
        #return ADD(super().__add__(other))
    def size(self):
        return len(self)
        
    def apply_filter(self,f):
        x=list(filter(f,self))
        return list_of_dictionaries(x)

    def apply(self,f):
        x=list(map(f,self))
        return list_of_dictionaries(x)
 ```
 See the vector object construction inhereted from list in [here](http://code.activestate.com/recipes/52272-vector-a-list-based-vector-class-supporting-elemen/) ([Backup]())

## Enrich dictionary to use `a['b']` as `a.b`
> The goal is to create a mock class which behaves like a db resultset.

From [here](https://stackoverflow.com/a/1328686/2268280): So what you want is a dictionary where you can spell a['b'] as a.b?

That's easy:

    class atdict(dict):
        __getattr__= dict.__getitem__
        __setattr__= dict.__setitem__
        __delattr__= dict.__delitem__

## `__setitem__` and `__getitem__`
