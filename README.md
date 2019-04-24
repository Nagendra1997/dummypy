## Mesibo Python API
Mesibo offers everything to make your app real-time and scalable for your first billion users and the next. It's modular, lightweight and easy to integrate.

Mesibo supports almost all popular platforms and languages for you to quickly build your applications. Whether you are developing mobile apps (Android, iOS, Java, Objective-C, C++), web apps (Javascript), integrating with backend (Linux, MacOS, Windows, Python, C++) or creating cool devices using Raspberry PI, mesibo has APIs for you.

Mesibo's high performance C++ and Python libraries enable you to interface your chat clients with various scientific computing and machine learning systems on your backend like TensorFlow, Matlab, Octave, NumPy etc to create a powerful chat experience.

This repo contains the source code for Mesibo Python API.

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



