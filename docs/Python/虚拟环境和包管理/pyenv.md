# pyenv

> [pyenv](https://github.com/pyenv/pyenv) is a Simple Python Version Management, lets you easily switch between multiple versions of Python(like nvm).

!!! tip

    To use pyenv on Windowns, use [`pyenv-win`](https://github.com/pyenv-win/pyenv-win)

## Install

```shell
brew install pyenv

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

## Commands

### List All Available Versions

```shell
pyenv install --list
```

### Install Specific Version

```shell
pyenv install <version>
```

### List Installed Versions

```shell
# Lists all Python versions known to pyenv, and shows an asterisk next to the currently active version.
pyenv versions
```

### Switch Versions

```shell
pyenv shell <version> # select just for current shell session
pyenv local <version> # automatically select whenever you are in the current directory (or its subdirectories)
pyenv global <version> # select globally for your user account
```

### Display Full Path to Executable

```shell
pyenv which python # display full path to executable that pyenv will invoke when you run the given command
```

### Uninstall

```shell
pyenv uninstall <version>
```

## pyenv-virtualenv

> [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv) is a pyenv plugin to manage virtualenv (a tool to create isolated Python environments).

### Install

```shell
brew install pyenv-virtualenv

echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
```

### List existing virtualenvs

```shell
pyenv virtualenvs
```

### Create a new virtualenv

```shell
pyenv virtualenv <python version> <virtual environment name>
```

### Activate a virtualenv

```shell
pyenv activate <virtual environment name>
pyenv deactivate
```

### Delete a virtualenv

```shell
pyenv uninstall <virtual environment name>
```
