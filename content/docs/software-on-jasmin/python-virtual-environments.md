---
aliases: /article/4489-python-virtual-environments
date: 2022-12-29 17:58:01
description: Python Virtual Environments
slug: python-virtual-environments
title: Python Virtual Environments
---

This article describes how you can use "virtual environments" to install
Python packages that are not provided in the [common software environments on
JASMIN]({{< ref "software-overview" >}}). You might wish to do this if you
want to use different packages/versions from those installed on the system, or
if you have requested for a package to be installed system-wide but wish to
start using it before this request can be acted upon.

To decide whether you should use a _Python virtual environment_ or a _Conda
environment_ for this purpose, see: [overview of software environments]({{<
ref "conda-environments-and-python-virtual-environments" >}}).

## What is a "virtual environment"?

A "virtual environment" is a self-contained directory tree that contains a
Python installation for a particular version of Python (such as 2.7, 3.7,
3.8), plus a number of additional packages. It provides a very useful method
for managing multiple environments on a single platform that can be used by
different applications.

## Creating a virtual environment

**As a pre-requisite, when using any modern Python (i.e. Python2.7 onwards),
you should[activate a Jaspy environment]({{< ref "quickstart-software-envs"
>}}) before following the instructions below.**

Python allows you to create a directory containing a private virtual
environment, into which you can install your packages of choice. This is done
differently for python2 and python3, as follows:

    
    
    # Python 3 onwards:
    python -m venv /path/to/my_virtual_env
    
    # Python 2.7
    virtualenv /path/to/my_virtual_env
    

The path can be an absolute or relative path, but it should not already exist.
Note: `/path/to/my_virtual_env` here (and also in the commands shown below)
should be replaced by the actual path where you choose to create your virtual
environment.

### Using the system "site-packages" with your virtual environment

Note that if you create a virtual environment using the above syntax, the
packages initially installed in it will **only be those in the standard Python
library**. This means, for example, that the `numpy` package (not in the
standard library, but installed as part of Jaspy) will be unavailable unless
you install it yourself. If you would prefer as a starting point to have all
the add-on packages which have already been installed in Jaspy, then use
instead:

    
    
    python -m venv --system-site-packages /path/to/my_virtual_env
    

This will work for most packages in Jaspy. We have seen situations where one
or two packages from Jaspy do not work in private virtual environments, and if
you are affected by this then please see the "package-specific fixes" section
below.

#### Activating a virtual environment

Before the virtual environment can be used, it needs to be " **activated** ".
This is done by running the `activate` script using the `source` command:

    
    
    source /path/to/my_virtual_env/bin/activate
    

(If you prefer, you can use `.` instead of `source`.)

After you run the activate script, some environment variables will be set so
that the `python` (or python2.7, python3) command will point to the one in the
virtual environment, allowing installation and use of packages in that
environment.

You can see that `python` points to the python executable in the virtual
environment, with:

    
    
    $ which python
    /home/users/my_username/my_virtual_env/bin/python
    

Note that you have to source the `activate` script in **every** shell (login
session) in which you intend to use the virtual environment. If there is a
particular virtual environment which you want to use consistently, you might
consider putting the command to source the `activate` script in your
`$HOME/.bashrc` file.

If you wish to deactivate the currently active virtual environment in a
particular shell, just type `deactivate`. The environment variable changes
will be undone, and you will again be using the system default set of
packages. This is also reflected in the shell prompt.

## Installing packages into a virtual environment

Once you have activated a virtual environment, the `pip` utility will be
available. This allows package installation into the environment using the
command:

    
    
    pip install your_package
    

`pip` is quite flexible what you can use for `your_package`. It can include:

  * a package name in the [Python Package Index](https://pypi.python.org/pypi) (PyPI)
  * a URL pointing to a package repository
  * the local path of a `.tar.gz` or `.zip` file containing the package source
  * the local path of a directory containing the extracted package source
  * the download URL of a `.tar.gz` or `.zip` file

If the package requires other packages that are not already installed into the
virtual environment, then `pip` will use the package's requirements file to
install them automatically from PyPI.

To upgrade an existing package, use:

    
    
    pip install --upgrade your_package
    

If your Python package cannot be installed with `pip` for any reason, it can
also be installed directly from the `setup.py` file after activating the
virtual environment.

    
    
    python setup.py install
    

To install a specific version of a package, this can be specified with:

    
    
    pip install your_package==1.2.3
    

## Inspecting the virtual environment

To list the packages installed into the virtual environment, with their
version numbers, type:

    
    
    pip freeze
    

## Using the virtual environment

### Interactive use

After you have activated the virtual environment in your shell, any packages
that you have installed into it can be imported into an interactive python
session.

    
    
    $ python # automatically uses python in your virtualenv
    
    >>> import my_package
    

### Scripts

If a script is run using the `python` command on the command-line in a similar
way to when starting an interactive Python session, this will use any virtual
environment that has been activated in the calling shell.

    
    
    $ python my_script.py
    

####

If an executable script is run using the `#!` mechanism, and the first line of
the script has the hard-coded path to the executable in the virtual
environment, then it is not necessary to activate the virtual environment in
the calling shell.

    
    
    $  head -n 1 myscript.py  # show the first line
    #!/path/to/my_virtual_env/bin/python3.7
    
    $  chmod u+x myscript.py  # ensure that it is executable
    
    $  ./myscript.py  # run it
    

As an alternative to hard-coding the path of the virtual environment, it is
possible to use the `/usr/bin/env` approach to ensure that the script is run
using whichever python executable is found via `$PATH`. The script will then
run using any virtual environment that has been activated in the calling
shell. This makes the script more portable, although at the expense of having
to source the activate script.

    
    
    $  head -n 1 myscript.py
    #!/usr/bin/env python3.7
    
    $  chmod u+x myscript.py
    
    $  ./myscript.py
    

## Package-specific fixes

When using the `--system-site-packages` option in combination with Jaspy, it
has been found that some packages provided by Jaspy (and which work correctly
in the Jaspy environment itself) require fixes in order to use them in virtual
environments that are created on top of Jaspy. In particular:

  * if you use `shapely`, we suggest to reinstall this into your virtual environment using `pip install --ignore-installed shapely` after activating the environment
  * if you use `geopandas`, you will need to reinstall shapely as above, and also when running python you will need to set an environment variable to enable it to find the `spatialindex` library. After loading Jaspy and activating the virtual environment, you could use either one of the following: 
    * `export LD_LIBRARY_PATH=$CONDA_PREFIX/lib:$LD_LIBRARY_PATH`
    * `export LD_PRELOAD=$CONDA_PREFIX/lib/libspatialindex.so:$CONDA_PREFIX/lib/libspatialindex_c.so`

Note that these environment variables could potentially also affect the
behaviour of other Linux commands, although unlikely, so you might prefer to
set them only for the python session (using a command of the form `env
variable_name=value python`) rather than using `export`.

  * if you use `cartopy` (also used by `iris`), you may need to create a symbolic link into your virtual environment to allow the correct loading of `libgeos_c.so` during `import cartopy` or `import iris`. To do this: 
    
        ln -s $CONDA_PREFIX/lib/libgeos_c.so /path/to/my_virtual_env/lib/
    	


