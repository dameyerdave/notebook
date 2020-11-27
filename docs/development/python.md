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
pipenv install python-dotenv

vi .env
export PS1="[\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\]]\$ "
export PYTHONPATH=.:$(pipenv --py)
export PIPENV_SKIP_LOCK=true

export FLASK_APP=icarus.py
export FLASK_ENV=development

pipenv shell
```

Set the venv python path in `.vscode/settings.json`:

```json
{
  "python.pythonPath": "$(pipenv --py)"
}
```

> **Hint:** You can also use `pipenv [--two | --three]` to use systems default python 2 or 3 version.

## Upgrade pipenv

```bash
brew upgrade pipenv
```

## Useful pipenv commands

### Update the packages

```bash
pipenv update
```

### Check for security issues

```bash
pipenv check
```

### Update a package to a specific version

```bash
pipenv package==1.0.0
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

## Pipenv configuration blocks

```ini
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]

[packages]

[requires]
python_version = "3.8"

[pipenv]
allow_prereleases = true
```

## Use a friendly logger

```bash
pipenv install friendlylog
```

```python
from friendlylog import colored_logger as log

# Anything above or including DEBUG will be logged.
log.setLevel(logging.DEBUG)

log.debug("debug message")
log.info("info message")
log.warning("warning message")
log.error("error message")
log.critical("critical message")
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

## Other tips and tricks

### `pip` install from a local repo

```bash
pip install -e path/to/repo
```

### Trick to install `pszcopg2`

```bash
env LDFLAGS='-L/usr/local/lib -L/usr/local/opt/openssl/lib -L/usr/local/opt/readline/lib' pipenv install psycopg2
```