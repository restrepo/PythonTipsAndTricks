## Numpy
### Set operations for 1D numeric arrays based on sorting.
<code>np.lib.arraysetops?
:Contains:
  ediff1d -> The differences between consecutive elements of an array.
  unique,
  intersect1d -> Return the sorted, unique values that are in both of the input arrays.
  setxor1d -> Return the sorted, unique values that are in only one (not both) of the
              input arrays.
  setdiff1d -> Return the sorted, unique values in `ar1` that are not in `ar2`
  in1d -> Test whether each element of a 1-D array is also present in a second array
  union1d -> Return the unique, sorted array of values that are in either of the two
             input arrays.</code>
             
         
## Tools and tricks
### Convert string to file object
<code>import io
fo=io.StringIO('[[1,2,3]]')</code>
### Convert  object (dict, lists,...) to recoverable string
<code>import json  
m = {'id': 2, 'name': 'hussain'}  
n = json.dumps(m)  
o = json.loads(n)  
print o['id'], o['name']</code>
### Similarity bewteen strings
<code>import Levenshtein
Levenshtein.ratio(s1,s2) # > 0.6</code>
### How to split a list or array into pairs in all possible ways
<code>
 In[1]: import itertools
 In[2]: a=[0,1,2] #or np.array(a)
 In[3]: list(itertools.combinations(a, 2))
Out[3]: [(0, 1), (0, 2), (1, 2)]
</code>