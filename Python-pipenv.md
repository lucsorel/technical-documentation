I mostly use python 3.x (for the use of generators and because 2.x will be deprecated in 2020).

# Pipenv

I manage project dependencies with pipenv, a tool wrapping `pip` and `virtualenv` to manage production and development dependencies.

Documentation about `pipenv`:
* https://realpython.com/pipenv-guide/
* https://pipenv.readthedocs.io/en/latest/
* https://jcutrer.com/howto/dev/python/pipenv-pipfile

## Install pipenv as a global library

```sh
curl https://raw.githubusercontent.com/kennethreitz/pipenv/master/get-pipenv.py | sudo python3
```

## Initialization of a python 3.x project

It links the installed python3 binary.

### Brand new project

```sh
export PIPENV_VENV_IN_PROJECT=true; pipenv --three
```

### From a requirements.txt file

From the [official documentation](https://pipenv.readthedocs.io/en/latest/basics/#importing-from-requirements-txt):

```sh
pipenv install -r path/to/requirements.txt
```

## Some commands

Library addition:

```sh
# add a production dependency
pipenv install numpy

# add a development dependency
pipenv install pylint --dev

# from a git/branch repo
pipenv install git+https://github.com/Ouest-France/sipy-logger.git@packaging#egg=sipy-logger
```
