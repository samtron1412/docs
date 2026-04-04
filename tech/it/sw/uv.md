# Overview

- https://docs.astral.sh/uv

# Pip interface

## Virtual Environments

- Create a new virtual environment:
    + `uv venv <env-name>`
    + `uv venv`: create a new virtual environment at the current folder
- Activate a virtual environment:
    + `source <path/to/bin/activate>`
        * `source rl-venv/bin/activate`
- Deactivate a virtual environment: `deactivate`
- Listing installed packages: `uv pip list`
- Show info about an installed package: `uv pip show numpy`
- Verifying an environment: `uv pip check`
    + Detect conflicting requirements from installed packages.

## Managing packages

### Installing a package

- `uv pip install <package-name>`
- Install from disk: `uv pip install "ruff @ ./projects/ruff"`
- Install from GitHub: `uv pip install "git+https://github.com/astral-sh/ruff"`
- Install from  a specific reference:

```
# Install a tag
uv pip install "git+https://github.com/astral-sh/[email protected]"

# Install a commit
uv pip install "git+https://github.com/astral-sh/ruff@1fadefa67b26508cc59cf38e6130bde2243c929d"

# Install a branch
uv pip install "git+https://github.com/astral-sh/ruff@main"
```

### Editable packages

- Editable packages do not need to be reinstalled for changes to their
  source code to be active.
    + Current directory: `uv pip install -e .`
    + In another directory: `uv pip install -e "ruff @ ./project/ruff"`

### Installing packages from files

- `uv pip install -r requirements.txt`
- `uv pip install -r pyproject.toml`

### Uninstalling a package

- `uv pip uninstall flask`

### Declaring dependencies

- `pyproject.toml`

```
[project]
dependencies = [
  "httpx",
  "ruff>=0.3.0"
]
```
