# pyenv

> pyenv is a Simple Python Version Management, lets you easily switch between multiple versions of Python(like nvm).

!!! tip

    To use pyenv on Windowns, use `pyenv-win`

## Install

```shell
brew install pyenv

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
source ~/.zshrc
```

## Commands

### Available Versions

```shell
pyenv install --list
```

### Install Specific Version

```shell
pyenv install <version>
```

### Switch Versions

```shell
pyenv shell <version> # select just for current shell session
pyenv local <version> # automatically select whenever you are in the current directory (or its subdirectories)
pyenv global <version> # select globally for your user account
```

### Uninstall

```shell
pyenv uninstall <version>
```
