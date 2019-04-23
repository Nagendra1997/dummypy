## Mesibo Python API
Mesibo Messenger is an open-source app with real-time messaging, voice and video call features.This repo contains the source code for Mesibo Python API.

- **Website:** https://mesibo.com
- **Documentation:** https://mesibo.com/documentation/

## Prerequisites
Build Mesbio Python modules requires the following software installed:

1.Python 3.4.x or newer
On Debian and derivatives (Ubuntu): python, python-dev (or python3-dev)
On Windows: the official python installer at www.python.org is enough

Make sure that the Python package distutils is installed before continuing. For example, in Debian GNU/Linux, installing python-dev also installs distutils.

2.Compilers
C extension modules for Python need a C compiler.GCC 4.x (and later) compilers are recommended. 


## Basic Installation
To install Mesibo Python API module

```
python setup.py install
```

To perform an in-place build that can be run from the source folder run:
```
python setup.py build_ext --inplace
```



