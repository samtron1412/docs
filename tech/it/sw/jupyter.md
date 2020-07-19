# Overview

Jupyter Notebook, a Python package


# Introduction

- `jupyter notebook`: a web-based interactive computational environment
  for multiple programming languages such as Python, etc.
- `jupyterlab`: next-generation of jupyter notebook

# Installation

- `conda install jupyter` or `pip install jupyter`
- `conda install -c conda-forge jupyterlab` or `pip install jupyterlab`

# Running

- Activate the conda environment if necessary
- `jupyter notebook`
- `jupyter lab`

# Securing a notebook server

- https://jupyter-notebook.readthedocs.io/en/stable/public_server.html
    + Set a password
    + etc.

# Usage

- Jupyter notebook: https://realpython.com/jupyter-notebook-introduction/
- Jupyter lab: https://towardsdatascience.com/jupyter-lab-evolution-of-the-jupyter-notebook-5297cacde6b

## IPython

- `!cd`: running the system command-line tools
    + These commands are executed in a temporary subshell.
- `%cd`: automagic functions, change the working directory in a more enduring way

# Tips and Tricks for jupyter notebook

## Export to PDF without section numbers

```nosecnum.tplx
((* extends 'article.tplx' *))

((* block commands *))
\setcounter{secnumdepth}{0} % Turns off numbering for sections
((( super() )))
((* endblock commands *))
```

`jupyter notebook --to=pdf --template=nosecnum.tplx file.ipynb`

## Install nbextensions

## Export to PDF with newpage break

- Add the following code to a raw NBConvert cell type:

```
%%latex
\newpage
```

## Export to HTML without code blocks (hide all input blocks)

`jupyter nbconvert <yourFile>.ipynb --no-input --no-prompt`
