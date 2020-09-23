# Python

## Install python
> To install `brew` goto [Install brew](../shell/brew.md#Install brew)

```bash
brew install python
```

## Upgrade python

```bash
brew upgrade python@3.8
```

## Create a virtual environment

```bash
brew install pipenv
pipenv --python /usr/local/bin/python3.8

vi .env
export PS1="[\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\]]\$ "
export FLASK_APP=icarus.py
export FLASK_ENV=development
export PYTHONPATH=.:$(pipenv --py)

pipenv shell
```