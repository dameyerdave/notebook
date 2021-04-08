# Brew

## Install brew

## Usefull installations

```bash
brew install coreutils
brew install wget
brew install gnu-sed
```

## Install `direnv`

```bash
brew install direnv

vi ~/.bashrc
export PS1="${CUSTOM_PS1:-[\[\033[36m\]\u\[\033[m\]@\[\033[32m\]noti:\[\033[33;1m\]\w\[\033[m\]]\$} "
eval "$(direnv hook bash)"

vi .envrc
export CUSTOM_PS1="\[\033[0;1;44m\](venv)\[\033[m\] [\[\033[36m\]\u\[\033[m\]@\[\033[32m\]noti:\[\033[33;1m\]\w\[\033[m\]]\$ "
export PYTHONPATH=.:/Users/davmeyer/.local/share/virtualenvs/icarus_be-w4UmfLn6/lib/python3.8/site-packages
export PIPENV_SKIP_LOCK=true
export PIPENV_VERBOSITY=-1
# export VIRTUAL_ENV_DISABLE_PROMPT=1

export FLASK_ENV=development
```
