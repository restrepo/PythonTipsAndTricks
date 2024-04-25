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
# Important extensions
## Widgets
`pip install ipywidgets jupyterlab_widgets`

Example
```python
radiobutton = widgets.RadioButtons(
    options=[True, False],
    value=False, # Defaults to 'pineapple'
#    layout={'width': 'max-content'}, # If the items' names are long
    description='New letter?',
    disabled=False
)
output_radiobutton = widgets.Output()
```
which can be used inside a jupyter notebook as:
```python
radiobutton.description = "Load Body?"
radiobutton.value = True
display(radiobutton,output_radiobutton)
```
![image](https://github.com/restrepo/PythonTipsAndTricks/assets/655883/eeab0416-46c0-4ca4-be01-75b23854ed9e)
Once selected, store with
`LOAD_BODY = radiobutton.get_interact_value()

## MyST
`pip install jupyterlab_myst`

Example

```{figure} https://source.unsplash.com/random/500x200/?mountain
:label: my-fig
:align: center

My **bold** mountain 🏔🚠.
```

Check out [](#my-fig)!!
