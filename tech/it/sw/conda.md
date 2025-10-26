# Overview

- Conda vs. Pip
    + https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/
- https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html
- conda
    + anaconda: a full distribution with a lot of binaries and libraries
    + miniconda: an empty conda environment, containing only Conda, its
    dependencies and python.

## Glossary

- `~/.condarc`: configure conda
    + run `conda config` to create one in the home directory
- Channels: the location of repositories where conda looks for packages

## General commands

- `conda <command> --help`
- `conda clean`: remove unused packages and cache
- `conda config`: modified values in .condarc
    + https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html
- `conda create`: create an environment
- `conda info`: show conda's information
- `conda list`: show a list of all packages
- `conda install`
- `conda package`
- `conda search`
- `conda remove`
- `conda update`

## Tasks

- https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/index.html

### Managing Channels

- Install a package from a non-default channel:
    + `conda install --channel conda-forge opencv`
- Add a new channel
    + `conda config --append channels conda-forge`
    + Or you can modify `~/.condarc`: the order of channels is matter,
    conda looks at these channel in order

```.condarc
channels:
  - defaults
  - conda-forge
channel_priority: strict
```

### Managing environments

- Activate an environment: `conda activate env_name`
- Deactivate: `conda deactivate`
- List all environments: `conda list --envs`
    + `conda env list`
- `conda init`: add some code to shellrc (.zshrc, etc.) to modify PATH
  when run conda activate
- Remove an environment: `conda env remove --name myenv`
- Create a new environment: `conda create --name myenv`
- Specify python version: `conda create -n myenv python=3.4`
- Specify default packages: `conda create -n myenv scipy`
- Specify version of a package: `conda create -n myenv scipy=0.15.0`
- Specify python and multiple packages
    + `conda create -n myenv python=3.4 scipy=0.15.0 astroid babel`
- No default packages: `conda create --no-default-packages -n myenv python`
- Building an identical environment using spec-file (usually is the same
  computer not for sharing)
    + `conda list --explicit > spec-file.txt`
    + `conda create --name myenv --file spec-file.txt`
- Sharing environments:
    + Export the active environment with all packages
        * `conda env export > environment.yml`
        * This way may not work across platforms because some of
        dependencies are different in different platforms.
    + Export only packages that you specifically install not all of its
    dependencies. The dependencies will be installed on the new platform
    later by conda.
        * `conda env export --from-history > environment.yml`
        * https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#exporting-an-environment-file-across-platforms
    + Creating an environment from an environment.yml file:
        * `conda env create -f environment.yml`

```environment.yml
name: stats2
channels:
  - javascript
dependencies:
  - python=3.4   # or 2.7
  - bokeh=0.9.2
  - numpy=1.9.*
  - nodejs=0.10.*
  - flask
  - pip:
    - Flask-Testing
```

- Restore an environment:
    + List the history of changes: `conda list --revisions`
    + Restore: `conda install --rev REVNUM`
        * `conda install --rev 8`
- Specify location for the environment:
    + `conda create --prefix /path/to/myenv jupyterlab=0.35 matplotlib=3.1 numpy=1.16`
    + Activate by name: `conda activate /path/to/myenv`
- Update an environment by modifying .yml file and run:
    + `conda env update -n conda-env -f /path/to/environment.yml`
    + `conda env update --prefix ./env --file environment.yml  --prune`
- Cloning an environment: `conda create --name myclone --clone myenv`


### Managing packages

- Activate an environment before installing a package
- Search a package: `conda search scipy`
- Install a package: `conda install scipy`
- Specific version: `conda install scipy=0.15.0`
- Update a package: `conda update scipy`
- View list of packages: `conda list`

### Managing python

- List all python versions: `conda search python`
    + `conda search --full-name python`
- Update python: `conda update python`

#### Create an environment with python 2.7

- `CONDA_SUBDIR=osx-64 conda create -n py27 python=2.7`
- Use it
    + `conda activate py27`
    + `python2 ...`: using `python2` command instead of just `python`

