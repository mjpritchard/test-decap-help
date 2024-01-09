---
aliases: /article/293-running-python-on-jasmin
categories:
- Software on JASMIN
collection: jasmin-documentation
date: 2021-11-16 09:40:35
description: Running python on JASMIN
slug: running-python-on-jasmin
tags:
- python
- JASMIN
- ImportError
- numpy
- import
- JAP
title: Running python on JASMIN
---

On the JASMIN analysis machines and on Lotus, we support Python2.7 and
Python3.7 through [Jaspy]({{< ref "jaspy-envs" >}}).

When you log in, the default version of Python is 2.7.5, which is used by the
operating system. If you require any packages other than the standard Python
library then you should use the Jaspy environments. In this example, we
activate the Python3.7 Jaspy environment before running python.

    
    
    $ module load jaspy/3.7
    

To run a python script you can then run:

    
    
    $ python your_script.py
    

If you want to use an executable script (which can be invoked just by name),
then the recommended line to put at the top of the script would be:

    
    
    #!/usr/bin/env python
    

after which you should set "write" permission, and then you can run it without
the "python " prefix:

    
    
    $ chmod 755 your_script.py
    $ ./your_script.py
    

Please note that the scientific software is not provided on the login nodes.
You first need to `ssh` to one of the "sci" analysis machines. For example:

    
    
    $ ssh -X jasmin-sci2
    ...
    $ module load jaspy/3.7
    $ python
    ...
    >>> import numpy
    >>>
    


