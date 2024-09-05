---
aliases: /article/293-running-python-on-jasmin
description: Running python on JASMIN
slug: running-python-on-jasmin
tags:
- python
- numpy
- import
- jap
- jaspy
title: Running python on JASMIN
---

On the JASMIN analysis machines and on Lotus, we currently support
Python version 3.10 through [Jaspy]({{% ref "jaspy-envs" %}}).

When you log in, the default version of Python is `2.7.5` which is the used by the
operating system. You shoud now use a more modern version of Python as v2.x is now deprecated. 
We recomment using the Jaspy environments. In this example, we
activate the current Jaspy environment before running Python.

{{<command user="user" host="sci1">}}
module load jaspy
{{</command>}}

Check the Python version:

{{<command user="user" host="sci1">}}
python -V
(out)Python 3.10.8
{{</command>}}

Run a script:

{{<command user="user" host="sci1">}}
python your_script.py
{{</command>}}

If you want to use an executable script (which can be invoked just by name),
then the recommended line to put at the top of the script would be:

```bash
#!/usr/bin/env python
```

after which you should set "write" permission, and then you can run it without
the "python " prefix:

{{<command user="user" host="sci1">}}
chmod 755 your_script.py
./your_script.py
{{</command>}}

You should work with Python on the [scientific analysis servers]({{% ref "sci-servers" %}}).
Login servers do not have any software installed, or filesystems mounted other than home directories.
