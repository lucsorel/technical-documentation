
# Python

I only use python 3.x (for the use of generators and because 2.x will be deprecated in 2020).

Some Ubuntu-based distributions are packaged with python3.6 and you may need a 3.7 version to be installed alongside in your system. I combine the use of [a PPA to install python 3.7](https://linuxize.com/post/how-to-install-python-3-7-on-ubuntu-18-04/) and the [configuration of `update-alternatives`](https://stackoverflow.com/questions/43062608/how-to-update-alternatives-to-python-3-without-breaking-apt) to allow switching between 3.6 and 3.7:

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
