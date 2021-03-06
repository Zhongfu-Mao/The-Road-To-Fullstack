# Poetry

> Poetry is a tool for **dependency management and packaging** in Python.  
> It allows you to declare the libraries your project depends on and it will manage (install/update) them for you.

[ðå®ç½](https://python-poetry.org/)

## å®è£

```zsh
# å®è£ poetry
curl -sSL https://install.python-poetry.org | python3 -
# åå¥ç¯å¢åé
vim ~/.zshrc
export PATH="/Users/<username>/.local/bin:$PATH"
source ~/.zshrc
```

## ä½¿ç¨

[ðCLIå½ä»¤](https://python-poetry.org/docs/master/cli/)

### è·åå¸®å©

```zsh
$ poetry [--help] # ææ²¡æ`--help`ææä¸æ ·ç
Poetry version 1.1.12

USAGE
  poetry [-h] [-q] [-v [<...>]] [-V] [--ansi] [--no-ansi] [-n] <command> [<arg1>] ... [<argN>]

ARGUMENTS
  <command>              The command to execute
  <arg>                  The arguments of the command

GLOBAL OPTIONS
  -h (--help)            Display this help message
  -q (--quiet)           Do not output any message
  -v (--verbose)         Increase the verbosity of messages: "-v" for normal output, "-vv" for more verbose output and "-vvv" for debug
  -V (--version)         Display this application version
  --ansi                 Force ANSI output
  --no-ansi              Disable ANSI output
  -n (--no-interaction)  Do not ask any interactive question

AVAILABLE COMMANDS
  about                  Shows information about Poetry.
  add                    Adds a new dependency to pyproject.toml.
  build                  Builds a package, as a tarball and a wheel by default.
  cache                  Interact with Poetry's cache
  check                  Checks the validity of the pyproject.toml file.
  config                 Manages configuration settings.
  debug                  Debug various elements of Poetry.
  env                    Interact with Poetry's project environments.
  export                 Exports the lock file to alternative formats.
  help                   Display the manual of a command
  init                   Creates a basic pyproject.toml file in the current directory.
  install                Installs the project dependencies.
  lock                   Locks the project dependencies.
  new                    Creates a new Python project at <path>.
  publish                Publishes a package to a remote repository.
  remove                 Removes a package from the project dependencies.
  run                    Runs a command in the appropriate environment.
  search                 Searches for packages on remote repositories.
  self                   Interact with Poetry directly.
  shell                  Spawns a shell within the virtual environment.
  show                   Shows information about packages.
  update                 Update the dependencies as according to the pyproject.toml file.
  version                Shows the version of the project or bumps it when a valid bump rule is provided.
```

### åå»ºæ°é¡¹ç®

#### æ éé¡¹

```zsh
$ poetry new my-package
Created package my_package in my-package

$ tree
.
âââ my-package
    âââ README.rst
    âââ my_package
    â   âââ __init__.py
    âââ pyproject.toml
    âââ tests
        âââ __init__.py
        âââ test_my_package.py

3 directories, 5 files
```

#### `--name`éé¡¹

```zsh
$ poetry new my-folder --name my-package
Created package my_package in my-folder

$ tree
.
âââ my-folder
    âââ README.rst
    âââ my_package
    â   âââ __init__.py
    âââ pyproject.toml
    âââ tests
        âââ __init__.py
        âââ test_my_package.py

3 directories, 5 files
```

#### `--src`éé¡¹

```zsh
$ poetry new --src my-package
Created package my_package in my-package

$ tree
.
âââ my-package
    âââ README.rst
    âââ pyproject.toml
    âââ src
    â   âââ my_package
    â       âââ __init__.py
    âââ tests
        âââ __init__.py
        âââ test_my_package.py

4 directories, 5 files
```

### å·²æé¡¹ç®

```zsh
cd pre-existing-project
poetry init
```

### æ·»å ä¾èµ

```zsh
poetry add <package-name>
```

### å®è£ä¾èµ

```zsh
poetry install
```

#### `--with`, `--without`, `--only`éé¡¹

```zsh
poetry install --with <group-name>
poetry install --without <group-name>
poetry install --only <group-name>
```

### åçº§ä¾èµ

```zsh
poetry update [<package-name>...]
```

### ç§»é¤ä¾èµ

```zsh
poetry remove <package-name> [--group <group-name>]
```

### æ¾ç¤ºä¾èµ

```zsh
poetry show [<package-name>]
```

### è®¾ç½®éç½®

```zsh
poetry config <key> <value>
poetry config --list
```

### å¯¼åºéå®æä»¶

```zsh
poetry export -f requirements.txt --output requirements.txt
```

## åçº§poetryèªèº«

```zsh
poetry self update <major.minor.patch>
```

## å¸è½½

```zsh
curl -sSL https://install.python-poetry.org | python3 - --uninstall
curl -sSL https://install.python-poetry.org | POETRY_UNINSTALL=1 python3 -
```

## å³é­èªå¨åå»ºèæç¯å¢

```zsh
poetry config virtualenvs.create false
```

## pyproject.toml

[ðææ¡£](https://python-poetry.org/docs/master/pyproject/)
