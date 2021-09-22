# Matplotlib
We assume that you already load a DataFrame, `df`, with columns: `x,y,z,..`
## Jupyter
Global configurations insides or outside the notebook
To use standard LaTeX 
```python
%pylab inline
from matplotlib import rc
rc('text', usetex=True)
rc('font',**{'family':'serif'})
```
## `plt` options
To be implemented in each plot. 
### Ticks control 
Classic configuration
```python
plt.tick_params(axis='both',direction='in',right=True,top=True)
plt.tick_params(which='minor',direction='in',right=True,top=True)
```
## Ticks options
### Select ticks to appear, e.g, in x-axis
`plt.xticks([1E2,1E4,1E6,1E8,1E10,1E12,1E14,1E16])`
### Ticks font size
`matplotlib.rcParams.update({'font.size': 15})`
## Fix PDF margins
`plt.tight_layout()`
## Label font size, position, etc.
```python
leg=plt.legend(prop={'size':13},loc=(0.33,0.6),...)
leg.set_title(r'${\cal L}\ [{\rm fb}^{-1}]$',prop={'size':20})
```

