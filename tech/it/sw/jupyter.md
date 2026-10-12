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

# Spark and EMR Notebook

## What is sparkmagic?

sparkmagic is a set of Jupyter tools (a kernel + a collection of %% magics like %%spark, %%sql, %%configure) that let a notebook talk to a remote Spark cluster over HTTP. The notebook process itself has no Spark in it. When you run a cell,
sparkmagic serializes the code, POSTs it to a REST endpoint, and the actual Spark driver runs over there on the cluster. Results come back as JSON.

That REST endpoint is Livy.

## What is the Livy kernel?

Apache Livy is a REST server that sits in front of Spark. It accepts "create a session" and "run this statement" calls over HTTP, manages the Spark driver lifecycle on the cluster (in YARN), and streams results back.

The "Livy kernel" (the PySpark/Spark kernels you see named pysparkkernel, sparkkernel) is just sparkmagic configured to point at a Livy server. So the chain is:

notebook cell ──HTTP──> Livy REST server ──> Spark driver (YARN) ──> executors
 (your laptop / kernel)        (on the cluster)

The driver lives on the cluster, decoupled from your notebook process.

## What does an EMR Notebook use?

"EMR Notebooks" (and the newer EMR Studio Workspaces) use exactly this sparkmagic + Livy model. The notebook server runs separately (in EMR Studio it's a managed Jupyter environment, fronted by Jupyter Enterprise Gateway), and code reaches
the cluster's Spark through Livy. You pick a PySpark / Spark kernel, which is sparkmagic underneath. The Spark driver runs on the cluster, not in your notebook kernel.

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
