## Installation
Fix the steps from https://jupyterbook.org/intro.html → 
Install the Python libraries needed to run the code in this particular example:

```bash
conda install numpy matplotlib
Install the pre-release for Jupyter Book

```bash
pip install -U jupyter-book --pre
Clone the repository containing the source files

```bash
git clone https://github.com/executablebooks/quantecon-mini-example
```

Run Jupyter Book over the source files

```bash
cd quantecon-mini-example/mini_book
jupyter-book build .
```
View the result through a browser — try (with, say, firefox)

```bash
firefox docs/_build/html/index.html
```
or

```bash
cd docs/_build/html
python -m http.server
```

and point your browser at the indicated port (e.g., localhost:8000).

## Edit cell tags
https://github.com/jupyterlab/jupyterlab/issues/4100#issuecomment-370866626
![cell edit](https://user-images.githubusercontent.com/1186124/37048553-3525e028-213c-11e8-83e7-2760446eab95.png)
## Convert with `jupytext`
```bash
jupytext --to markdown file.ipynb
jupytext --to notebook file.md
```
