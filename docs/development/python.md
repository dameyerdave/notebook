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

## Use migrations for `mongoengine`

1. Install `mongoengine-migrate`

```bash
pip install mongoengine-migrate
```

2. Make migrations from a file

```bash
mongoengine-migrate makemigrations -m module.py
```

3. Migrate mongodb

```bash
mongoengine-migrate migrate
```

or

```bash
mongoengine-migrate migrate previous_migration
```

## Resolve `pylint` not resolvable local imports

Edit `settings.json` inside the `.vscode` folder:

```json
{
    "python.analysis.extraPaths": ["./sources"]
}
```

## `pip` install from a local repo

```bash
pip install -e path/to/repo
```

## Regenerate `Pipfile` from `requirements.txt`

```bash
pip freeze > requirements.txt
pipenv install -r requirements.txt
rm -f requirements.txt
```

## Create a pipenv from a project

Inside your projects directory:

```bash
pipenv shell
pipenv install
```

## Update a package using `pipenv`

```bash
pipenv update <package>
```

## Install multiple python versions on mac using `homebrew`

```bash
brew update
brew install pyenv
pyenv install 3.7.4
pyenv versions
```

> set the pipenv python version

```bash
pipenv install --python ~/.pyenv/versions/3.7.4/bin/python
```

## Trick to install `pszcopg2`

```bash
env LDFLAGS='-L/usr/local/lib -L/usr/local/opt/openssl/lib -L/usr/local/opt/readline/lib' pipenv install psycopg2
```