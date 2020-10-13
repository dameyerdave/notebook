# Visual Code

## Configure Visual Code in general

## Configure Visual Code for Python

### Install the following extensions

- [ ] Pylance

### Install and configure `pipenv`

1. Upgrade python

```bash
brew upgrade python@3.8
```

2. Install `pipenv`

```bash
brew install pipenv
```

3. Create `pipenv`

```bash
pipenv --python /usr/local/bin/python3.8
```

4. Install packages

```bash
pipenv install <package>
```

Or if you already have a `requirements.txt` file

```bash
pipenv install -r requirements.txt
```

To also include `setup.py`

```bash
pipenv install -e .
```

5. Configure the environment

```bash
vi .env
export PS1="[\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\]]\$ "
export FLASK_APP=icarus.py
export FLASK_ENV=development
export PYTHONPATH=.:$(pipenv --py)
```

6. Jump into the pipenv

```bash
pipenv shell
```

## Configure Visual Code for Vue

## Configure Visual Code for React-Native
