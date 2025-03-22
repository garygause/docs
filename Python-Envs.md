# Python Environments Cheatsheet

There are a lot of choices these days for python virtual environments. This cheatsheet covers the basics of all of them so I can easily switch between when working with different teams. No favorites here!

- pipenv
- poetry
- venv
- conda
- virtualenv

# Pipenv

Reference: [Pipenv](https://pipenv.pypa.io/en/latest/)

Pipenv uses pip for dependency management and virtualenv for creating virtual environments.

Install:

```bash
pip install --user pipenv
```

Create env or activate:

```bash
pipenv shell
```

Deactivate:

```bash
exit
```

Add dependencies:

```bash
# normal install
pipenv install langchain

# install specific version
pipenv install langchain==0.2.1

# install as dev dependency
pipenv install pytest --dev

# install all dependencies
pipenv install

# install all plus dev dependencies
pipenv install --dev
```

Remove dependencies:

```bash
# remove dependency
pipenv uninstall langchain

# remove all dev dependencies
pipenv uninstall --all-dev

# remove all dependencies
pipenv uninstall --all
```

Update dependencies:

```bash
# update all dependencies
pipenv update

# update specific dependency
pipenv update langchain
```

Create lockfile (Pipfile.lock):

```bash
pipenv lock
```

Use with requirements.txt:

```bash
pipenv lock --requirements > requirements.txt
```

```bash
pipenv install --requirements requirements.txt
```

Locate the virtual environment:

```bash
pipenv --venv
```

Delete the virtual environment:

```bash
pipenv --rm
```

# Poetry

Reference: [Poetry](https://python-poetry.org/)

Install:

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

Create env or activate:

```bash
poetry shell
```

Usage:

```bash
# add dependency
poetry add langchain

# install specific dependency
poetry install langchain==0.2.1

# add dev dependency
poetry add pytest --dev

# install all dependencies
poetry install

# install all plus dev dependencies
poetry install --dev
```

Locate the virtual environment:

```bash
poetry env info
```

Delete the virtual environment:

```bash
poetry env remove
```

# venv

Reference: [venv](https://docs.python.org/3/library/venv.html)

Create env or activate:

```bash
python -m venv myenv
source myenv/bin/activate
```

Usage:

```bash
pip install langchain
...
```

# conda

Reference: [conda](https://docs.conda.io/en/latest/)

Create env or activate:

```bash
conda create -n myenv
```

Usage:

```bash
conda install langchain
```

# virtualenv

Reference: [virtualenv](https://virtualenv.pypa.io/en/latest/)

Create env or activate:

```bash
python -m venv myenv
source myenv/bin/activate
```

Usage:

```bash
pip install langchain
...
```
