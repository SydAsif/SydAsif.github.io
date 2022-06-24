---
layout: single
title:  "Python: Installation, Pip and Help function"
date:   2021-06-19 11:02:15 +0500
categories: python
tag: python
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## [What is python?](https://wiki.python.org/moin/BeginnersGuide/Overview)
Python is a clear and powerful object-oriented programming language, comparable to Perl, Ruby, Scheme, or Java.

### Some of Python's notable features

- Uses an elegant syntax, making the programs you write easier to read.
- Is an easy-to-use language that makes it simple to get your program working.
- Python ideal for prototype development and other ad-hoc programming tasks.
- Comes with a large standard library that supports many common programming tasks such as connecting to web servers, searching text with regular expressions, reading and modifying files.
- Python's interactive mode makes it easy to test short snippets of code.
- Runs anywhere, including Mac OS X, Windows, Linux, and Unix.
- Is free software in two senses. It doesn't cost anything to download or use Python.

### Some programming-language features of Python are

- A variety of basic data types are available: numbers, lists, and dictionaries.
- Python supports object-oriented programming with classes and multiple inheritances.
- Code can be grouped into modules and packages.
- The language supports raising and catching exceptions, resulting in cleaner error handling.
- Python contains advanced programming features such as generators and list comprehensions.

## [Downloading Python](https://wiki.python.org/moin/BeginnersGuide/Download)

Before you start, you will need Python on your computer.

Check whether you already have an up to date version of Python installed by entering python in a command line window. If you see a response from a Python interpreter it will include a version number in its initial display.

```console
[$] <> python3
Python 3.8.10 (default, Mar 15 2022, 12:22:08) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

If you need to install Python, you may as well download the most recent stable version. This is the one with the highest number that isn't marked as an alpha or beta release. Please see the [Python downloads page](https://www.python.org/downloads/) for the most up to date versions of Python. They are available via the yellow download buttons on that page.

## [What is pip?](https://pypi.org/project/pip/)

Pip is the package installer for Python. You can use pip to install packages from the Python Package Index and other indexes.

### [Installation](https://pip.pypa.io/en/stable/installation/)

Usually, pip is automatically installed if you are:

- working in a virtual environment
- using Python downloaded from python.org
- using Python that has not been modified by a redistributor to remove ensurepip

#### Supported Methods

If your Python environment does not have pip installed, there are 2 mechanisms to install pip supported directly by pip’s maintainers:

- ensurepip
- get-pip.py

#### Alternative Methods

Depending on how you installed Python, there might be other mechanisms available to you for installing pip such as using [Linux package managers](https://packaging.python.org/en/latest/guides/installing-using-linux-tools/#installing-pip-setuptools-wheel-with-linux-package-managers).

### [Debian/Ubuntu](https://packaging.python.org/en/latest/guides/installing-using-linux-tools/#id7)

On Ubuntu it's come pre-installed if not install with below command:

```console
sudo apt update
sudo apt install python3-venv python3-pip
```

> To check install modules via pip use `pip list` and to check pip version use `pip --version` commands.

## [Installing Python Modules](https://docs.python.org/3.8/installing/index.html)

As a popular open source development project, Python has an active supporting community of contributors and users that also make their software available for other Python developers to use under open source license terms. Pip is the preferred installer program. Starting with Python 3.4, it is included by default with the Python binary installers.

### Basic usage

The following command will install the latest version of a module and its dependencies from the Python Packaging Index.

`python3 -m pip install SomePackage`

It’s also possible to specify an exact or minimum version directly on the command line, the package name and the version.

`python -m pip install SomePackage==1.0.4    # specific version`

Upgrading existing modules or pip must be requested explicitly.

 `python3 -m pip install --upgrade SomePackage`

## help() function in Python

The Python help function is used to display the documentation of modules, functions, classes, keywords, etc.

The help function has the following syntax:

```console
[$] <> python3
Python 3.8.10 (default, Mar 15 2022, 12:22:08) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> help('print')

Out put as below:

```console
Help on built-in function print in module builtins:

print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.

```

If the help function is passed without an argument, then the interactive help utility starts up on the console.

```console
[$] <> python3
Python 3.8.10 (default, Mar 15 2022, 12:22:08) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> help()

Welcome to Python 3.8's help utility!

If this is your first time using Python, you should definitely check out
the tutorial on the Internet at https://docs.python.org/3.8/tutorial/.

Enter the name of any module, keyword, or topic to get help on writing
Python programs and using Python modules.  To quit this help utility and
return to the interpreter, just type "quit".

To get a list of available modules, keywords, symbols, or topics, type
"modules", "keywords", "symbols", or "topics".  Each module also comes
with a one-line summary of what it does; to list the modules whose name
or summary contain a given string such as "spam", type "modules spam".

help> 
```

The help function has the following syntax to check module.

`help> telnetlib` help utility output as below:

```console
Help on module telnetlib:

NAME
    telnetlib - TELNET client class.

MODULE REFERENCE
    https://docs.python.org/3.8/library/telnetlib
    
    The following documentation is automatically generated from the Python
    source files.  It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations.  When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    Based on RFC 854: TELNET Protocol Specification, by J. Postel and
    J. Reynolds
    
    Example:
    
    >>> from telnetlib import Telnet
    >>> tn = Telnet('www.python.org', 79)   # connect to finger port
    >>> tn.write(b'guido\r\n')
    >>> print(tn.read_all())
```

## dir() method in Python

The python dir() method returns the list of valid attributes of the passed object as below:

### dir() syntax

The syntax of `dir()` method is `dir('object')`.

- **object** can be an empty/filled tuples, list, set, dictionary etc or any user-defined object.

```py
>>> number = 12
>>> dir('number')
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```

```py
>>> string = 'Hello'
>>> dir('string')
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
>>> 
```

[PythonIDE](https://wiki.python.org/moin/IntegratedDevelopmentEnvironments)

[PythonEditor](https://wiki.python.org/moin/PythonEditors)
