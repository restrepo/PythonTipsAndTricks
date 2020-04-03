# Jupyter

## Jupyter notebook clear cell output in code

See https://stackoverflow.com/a/24818304/2268280
```python
from IPython.display import clear_output

for i in range(10):
    clear_output(wait=True)
    print("Hello World!")
```
# Save jupyter notebook command
```python
%%javascript
IPython.notebook.save_notebook()
```
