
# Python

I only use python 3.x (for the use of generators and because 2.x will be deprecated in 2020).

I have used 2 dependency management tools: Pipenv (which I don't use anymore) and Poetry (which I recommend).

## Python version switching

### Pyenv (local python version)

Prerequisites (see [common build problems](https://github.com/pyenv/pyenv/wiki/Common-build-problems)):

```sh
sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev python-openssl git
```

Pyenv installs the binaries of the versions on-demand, and allows to specify a python version for any folder.
It intercepts the calls to python & its libs and redirects them to the specified binaries.

#### Installation

Main doc page: [Pyenv installation documentation](https://github.com/pyenv/pyenv#installation).

* Linux: use the [automatic installation](https://github.com/pyenv/pyenv-installer)
* Mac (via Brew):

```sh
# installs pyenv
brew update
brew install pyenv

# append the following lines in your ~/.zshrc to activate pyenv in zsh terminals
# (see step 3 of https://github.com/pyenv/pyenv#basic-github-checkout for other shells)
if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init -)"
fi
```

#### Specify a python version in a project folder

```sh
# lists all the versions that can be installed (long list!)
pyenv install -l

# lists all the 3.8 versions that can be installed
pyenv install -l | grep "3.8"

# installs python 3.8.6 binaries on your system once
pyenv install 3.8.6

cd my-projects/project
pyenv local 3.8.6
# -> it creates a '.python-version' file. Version this file, to document & enforce the python version used in the project)
```

See the documentation of [pyenv's commands](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md).

### update-alternatives [unadvised: can easily break your system]

Some Ubuntu-based distributions are packaged with python3.6 and you may need a 3.7 version to be installed alongside in your system.
I combine the use of [a PPA to install python 3.7](https://linuxize.com/post/how-to-install-python-3-7-on-ubuntu-18-04/) and the [configuration of `update-alternatives`](https://stackoverflow.com/questions/43062608/how-to-update-alternatives-to-python-3-without-breaking-apt) to allow switching between 3.6 and 3.7 (but I recommend NOT DOING it anymore):

```sh
# adds the alternatives for python3 and python3m (lowest priority is chosen by default)
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 3
sudo update-alternatives --install /usr/bin/python3m python3m /usr/bin/python3.6m 2
sudo update-alternatives --install /usr/bin/python3m python3m /usr/bin/python3.7m 3

# manually chooses an alternative
sudo update-alternatives --config python3
sudo update-alternatives --config python3m

# installs pip
sudo apt-get install python3-pip

# installs the pip version adapted to version 3.7
python3.7 -m pip install pip
```

# Dependency management

## Poetry

### Install poetry

To make sure you install poetry for the appropriate python version (2.x or 3.5+), install it from a folder where `python --version` outputs the appropriate version. Then you can [install poetry](https://python-poetry.org/docs/#installation) on your system:

```sh
# we love executing scripts from the web...
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python

# append the following lines in your ~/.zshrc file to add poetry in your zsh terminal
export PATH="$HOME/.poetry/bin:$PATH"
```

[Update poetry](https://python-poetry.org/docs/#updating-poetry) binary:
```sh
poetry self update
```

### Local virtual environment

Add the following section in the generated `pyproject.toml` file to create a virtual environment and to locate it within the project folder (makes libraries' documentation browsing and docker image generation easier):
```toml
[virtualenvs]
create = true
in-project = true
```

### Initialize a project

See [project setup](https://python-poetry.org/docs/basic-usage/#project-setup) (make sure the `python --version` is the correct one).


### Add poetry management to an existing project

```sh
# defines the python version to use
pyenv local 3.7.6

# configures poetry for the project
export POETRY_VIRTUALENVS_CREATE=true
export POETRY_VIRTUALENVS_IN_PROJECT=true
poetry init
```

### Project setup

To ease the onboarding of colleagues or build docker images, I often use the following `init.sh` script:

```sh
#! /bin/sh

pythonbin='python3'
depsinstall='install --no-dev'

while getopts dp: OPTION "$@"; do
    # echo "option ${OPTION}"
    case $OPTION in
        # also installs development dependencies
        d)
            depsinstall='install'
            ;;
        # specifies the python binary used when installing poetry
        p)
            pythonbin=${OPTARG}
            ;;
        \?)
            echo "Invalid option: -$OPTION" >&2
            ;;
    esac
done

# installs poetry (for a non-docker environment)
if ! type "poetry" > /dev/null; then
    getpoetrycommand="curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | ${pythonbin}"
    echo "$(date '+%Y-%m-%d_%H:%M:%S') ${getpoetrycommand}"
    eval "${getpoetrycommand}"
    # makes poetry available in current shell
    . $HOME/.poetry/env
fi

echo "$(date '+%Y-%m-%d_%H:%M:%S') $(poetry --version) will be used to install dependencies"

# installs the project dependencies
export POETRY_VIRTUALENVS_CREATE=true
export POETRY_VIRTUALENVS_IN_PROJECT=true
echo "$(date '+%Y-%m-%d_%H:%M:%S') poetry ${depsinstall}"
poetry ${depsinstall}
```

There are 2 installation flags:
* `-p` unables to specify the python binary name (`python` or `python3`)
* `-d` also installs development dependencies (along the production ones) defined in the `pyproject.toml` file

## Pipenv [not recommended: slow]

I manage project dependencies with pipenv, a tool wrapping `pip` and `virtualenv` to manage production and development dependencies.

Documentation about `pipenv`:
* https://realpython.com/pipenv-guide/
* https://pipenv.readthedocs.io/en/latest/
* https://jcutrer.com/howto/dev/python/pipenv-pipfile

### Install pipenv as a global library

```sh
curl https://raw.githubusercontent.com/kennethreitz/pipenv/master/get-pipenv.py | sudo python3
```

### Initialization of a python 3.x project

It links the installed python3 binary.

#### Brand new project

```sh
export PIPENV_VENV_IN_PROJECT=true; pipenv --three
```

#### From a requirements.txt file

From the [official documentation](https://pipenv.readthedocs.io/en/latest/basics/#importing-from-requirements-txt):

```sh
pipenv install -r path/to/requirements.txt
```

### Some commands

Library addition:

```sh
# add a production dependency
pipenv install numpy

# add a development dependency
pipenv install pylint --dev

# from a git/branch repo (should be installed in editable mode to ensure an up-to-date copy of the repository and that it includes all known dependencies)
pipenv install -e git+https://github.com/Ouest-France/sipy_logger.git@packaging#egg=sipy_logger
```

Library removal:

```sh
# production, development and git dependendy are removable with the same command format
pipenv uninstall numpy
pipenv uninstall pylint
pipenv uninstall sipy_logger
```
