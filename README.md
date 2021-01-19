# Pipenv
pipenv is a package management system with virtual environment in python. It is built on the top of pip and virtual env. It is used to manage isolated python packages for every single project maautomatically managed by a virtual environment created by Pipenv.

This README describes How to install python and manage multiple version of python using pyenv (which is a python version manager - helps to manage multiple python versions). Then command-line cheat sheet of pipenv.

## Used Machine and Approach

1. Ubuntu 20.04 LTS
2. Non root sudo user

## Installing Pyenv
Pyenv is a python package manager that can be used to manage multiple versions of python on a single OS. Let's install pyenv latest version.

1. `$ sudo apt update -y` to update the system.
2. `$ sudo apt install -y build-essential` install the build dependencies.
3. `$ sudo apt install zlib1g-dev libssl-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl`
4. `$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv` to clone the latest version of git.
5. `$ sudo echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc`
6. `$ sudo echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc`
7. `$ sudo echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n eval "$(pyenv init -)"\nfi' >> ~/.bashrc`
8. `$ exec "$SHELL"`
9. `$ pyenv --version`. Now pyenv is installed successfully.

Learn more about pyenv: https://realpython.com/intro-to-pyenv/

## Installing Python
**Note:** The python version to be installed depend on the version that require the application. We can install multiple version of python and switch back to specific verion for our specific python version.

1. `$ pyenv install --list` to see all the available python version.
2. `$ pyenv install x.x.x` to install the needed version. We can install multiple versions. We can activate specific version when we need to create a virtual environment for a specific application.
3. `$ pyenv versions` to see installed/available version to activate.
4. `$ pyenv global x.x.x` to activate a specific python version locally.
5. `$ pyenv global system` switch back to system version.

## Installing Pipenv

1. Before installing Pipenv make sure python and pip is already installed (`$ python -V, python3 -V` and `$ pip --version, pip3 --version`).
2. If you are using multiple versions of python using pyenv then switch to the version of python that you want to work with Pipenv first (`$ pyenv global x.x.x`).
3. `$ pip install --user pipenv` to install pipenv.
4. `$ pipenv --version` to check the version.
5. `$ pip install --user --upgrade pipenv` to upgrade Pipenv anytime.

# Pipenv Cheat Sheet

1. Open up `~/.bashrc` file `$ nano ~/.bashrc` and add the line (`export PIPENV_VENV_IN_PROJECT=1`) at the bottom of the file. Save and exit.
2. `$ source ~/.bashrc` to take effect of the changes.
3. The above commands enable pipenv to create virtual environment (venv) in the current project directory (as `.venv`) rather that user directory.
4. If you want to roll back to default remove the line `export PIPENV_VENV_IN_PROJECT=1` from the `~/.bashrc` file. and then `$ source ~/.bashrc` and then `$ unset PIPENV_VENV_IN_PROJECT`.

5. Create or clone a project. `$ cd project-dir`
6. `$ pipenv install` will install a virtual envs first if already not exists then all the dependencies will be installed and also two additional files will be created `Pipfile` and `Pipfile.lock`. (Before run the command switch to the python version you want to create a venv on using pyenv)
7. `$ pipenv install pkg-name` will install the latest version of specified package in the current project's virtual environment (not system wide) and also added in the `Pipfile` in the normal dependencies section called [packages].
8. The Pipfile is very handy, when the project is shared with others or deploying from local to production then using Pipfile we can easily install all the dependencies very easily.
9. `$ pipenv install "pkg-name<=x.x.x"` to install specific version that is also pinned in the Pipfile.
10. `$ pipenv update --outdated` to see the current version and latest available version of every single packages installed inside the venv.
11. `$ pipenv update <pkg>` to update individual or `$ pipenv update` to update all packages. **Note:** Packages that are pinned as "*" in the Pipfile will be updated only.
12. If in your project directory presents any requirements.txt file. `$ pipenv install` command automatically install all the dependencies and convert that to Pipfile. Or manally can be installed by `$ pipenv install -r /path/to/requirements.txt`.
13. `$ pipenv install dev-pkg-name --dev` to install dev dependencies.
14. `$ pipenv install --ignore-pipfile` and `$ pipenv install --skip-lock` just install the virtual environment and ignore the Pipfile and does not install the dependencies if already exists in the dir.
15. **`$ pipenv shell` to activate the virtual environment. That means we can do all the thing in our virtual environemnt without activating the venv using pipenv command. That is awesome.**
16. **To deactivate the venv type:** `$ exit`.

17. `$ pipenv uninstall pkg-name` to uninstall specific package.
18. `$ pipenv uninstall --all-dev` to uninstall all dev packages.
19. `$ pipenv uninstall --all` to install all packages including dev dependencies. It will delete all the packages from the venv but the package names are still in the Pipfile. Because we want to delete all the packages. Not from the Pipfile that we need to setisfy the project dependencies.
20. `$ pipenv install` to install the project dependencies again specified in the Pipfile.


21. `$ pipenv graph` to see all the dependencies package for every individual packages. 
22. `$ pipenv check` to check the environment.
23. `$ pipenv --venv` to see the location of current venv.
24. `$ pipenv --where` to see current project dir.
25. `$ pipenv --rm` to uninstall or remove the current virtual environment.
