# How to Publish to PyPi

## Dependencies 
setuptools, wheel, twine <br>
Install them using <br>
```pip install setuptools, wheel, twine```

## Project Structure (├ ─ │ └ ) <br>

package <br>
├─ package/ <br>
│   ├─ __init__.py <br>
│   └─ main.py <br>
├── setup.py <br>
└── README.md <br>

## Setup.py
Have some boiler plate code, remove cythonize things if you don't cythonize anything <br>
```py
from setuptools import setup
from Cython.Build import cythonize

setup(
name="package_name",
version="0.0.1",
packages=["package_name"],
install_requires = ["pandas"],
ext_modules=cythonize(["package_name/file_name.pyx"], language_level=3),
)
```

## Create MANIFEST.in if you are using cythonize
```MANIFEST.in
include package_name/*.pyx
include package_name/*.pxd
```

## Run the setup 
```pip install build```
```python -m build```
you will see a wheel file in dist/ folder <br>
```pip istall package_name...*.whl```
to test your package in a sandbox env 

## Add console commands
To add console commands you need to change setup.py
```setup.py
setup(
...
    entry_point(
    "console_scripts":[
        "command_name": "package_name::function_name"
    ]
)
)
```
## Upload
``` twine upload dist/*

