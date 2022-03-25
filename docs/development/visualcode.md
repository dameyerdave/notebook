# Visual Code

## Configure Visual Code in general

## Configure Visual Code for Python

```json
{
  "python.terminal.activateEnvironment": false
}
```

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

## Configure prettier / eslint

in `.prittierrc.json`

```json
{
  "printWidth": 110,
  "trailingComma": "es5",
  "semi": true,
  "jsxSingleQuote": true,
  "singleQuote": true,
  "arrowParents": "avoid",
  "quoteProps": "consistent"
}
```

in `settings.json`

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true
}
```

in `package.json`

```json
"scripts": {
    "format": "prettier --write . && npx eslint . --fix",
    "check-format": "prettier --check .",
    "check-types": "tsc --noEmit"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ],
    "plugins": [
      "unused-imports"
    ],
    "rules": {
      "no-unused-vars": "off",
      "unused-imports/no-unused-imports": "error",
      "unused-imports/no-unused-vars": [
        "warn",
        {
          "vars": "all",
          "varsIgnorePattern": "^_",
          "args": "after-used",
          "argsIgnorePattern": "^_"
        }
      ]
    }
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
```