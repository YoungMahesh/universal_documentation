### using poetry (auto-track dependencies)
- [installation](https://python-poetry.org/docs/#installing-with-the-official-installer)
```bash
# create new project, pyproject.toml will contain list of dependencies
poetry new <project-name>

poetry add <module-name> # install package/module

poetry install # install dependencies

poetry run <package-name>

poetry env activate
poetry env info # get information about currently activated environment
poetry env info --path
poetry env list
poetry env list --full-path
poetry env remove /full/path/to/python
poetry env use /full/path/to/python

poetry self update
```

### default using virtual environment

```bash
# python: Invokes the Python interpreter
# -m: Runs a Python module as a script
# venv: The built-in Python module for creating virtual environments
# .venv (at end): The name of the directory where the virtual environment will be created
python -m venv .venv

# Activate the virtual environment (On Linux):
# source <myproject_env>/bin/activate 
source venv/bin/activate
# above command will create following environment
# venv/
# ├── bin/           # Activation scripts (Unix/macOS)
# │   ├── activate
# │   └── python
# ├── Scripts/       # Activation scripts (Windows)
# │   ├── activate
# │   └── python.exe
# ├── lib/           # Isolated Python libraries
# └── pyvenv.cfg     # Configuration file 

# install packages while keeping track which packages with which version are installed
# create requirements.txt, list packages in it like and install packages
gradio==5.15.0
pip install -r requirements.txt

# write your code in app.py and execute it
python app.py

# deactivate currently active environment
deactivate 
```