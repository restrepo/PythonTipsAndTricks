# Mathplotlib
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
