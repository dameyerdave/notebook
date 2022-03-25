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

## Safety check (security audit)
```bash
pip install safety
safety check
```

## Create a virtual environment

```bash
brew install pipenv
pipenv --python /usr/local/bin/python3.8
pipenv install python-dotenv

vi .envrc
export CUSTOM_PS1="\[\033[0;1;44m\](venv)\[\033[m\] [\[\033[36m\]\u\[\033[m\]@\[\033[32m\]noti:\[\033[33;1m\]\w\[\033[m\]]\$ "
export PYTHONPATH=.:$(pipenv --py)
export PIPENV_SKIP_LOCK=true
export PIPENV_VERBOSITY=-1
# export VIRTUAL_ENV_DISABLE_PROMPT=1

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

## Generate `Pipfile` from `requirements.txt`

```bash
pip freeze > requirements.txt
pipenv install -r requirements.txt
rm -f requirements.txt
```

## Generate `requirements`.txt from `Pipfile`

```bash
pipenv lock -r > requirements.txt
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

## Install a package directly from git

```bash
pipenv install -e git+https://github.com/dameyerdave/mongoengine-history.git#egg=mongoengine_history
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
    "python.pythonPath": "$(pipenv --py)",
    "python.analysis.extraPaths": ["${workspaceFolder}/<python source>"],
}
```

## Additional settings for `vscode`

```json
{
    "python.envFile": "${workspaceFolder}/<python source>/.env",
    "python.linting.flake8Enabled": true,
    "python.linting.pylintEnabled": false,
    "python.linting.enabled": true,
    "python.terminal.activateEnvironment": false,
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    }
    
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

## Create a pypi package

&rarr; [How to](https://dzone.com/articles/executable-package-pip-install)

1. Install required software

```bash
pipenv install setuptools wheel tqdm twine
```

2. Create a `setup.py` file:

```python
import setuptools

with open('README.md', 'r') as fh:
    long_description = fh.read()

setuptools.setup(
    name='package-name',
    version=0.1,
    author='David Meyer',
    author_email='dameyerdave@gmail.com',
    description='Python Rules Evaluator',
    long_description=long_description,
    long_description_content_type='text/markdown',
    python_requires='>=3.5',
    url='https://github.com/dameyerdave/python-rules-evaluator',
    packages=setuptools.find_packages(exclude='test'),
    classifiers=[
        'Programming Language :: Python :: 3',
        'License :: OSI Approved :: MIT License',
        'Operating System :: OS Independent'
    ],
    install_requires=[
        'pyyaml',
        'friendlylog'
    ],
    entry_points={
        'console_scripts': {
            'command = package.module:method'
        }
    }

)
```

3. Create a module

```bash
mkdir python-rules-evaluator
cd python-rules-evaluator
touch __init__.py
```

4. Compile the package

```bash
python setup.py sdist bdist_wheel
```

4. Install it on your local machine

```bash
pipenv install dist/*.whl
```

5. Create a `~/.pypirc` file

```ini
[distutils]
index-servers=pypi
[pypi]
repository = https://upload.pypi.org/legacy/
username = dameyerdave
```

6. Upload it to `pypi.org`

```bash
twine upload dist/*
```