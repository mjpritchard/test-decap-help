---
aliases: /article/121-sci-servers
date: 2022-11-16 08:49:22
description: Scientific analysis servers
slug: sci-servers
tags:
- scientific
- analysis
- machine
- sci
- jasmin-sci
- jap
- platform
- Arbiter
- 'fatal: Could not read from remote repository'
- git
title: Scientific analysis servers
---

Once you have logged on to one of the [login servers]({{< ref "login-servers" >}}) you can then `ssh` a scientific analysis (sci) server to do your work.

## Available sci servers

Access to the scientific analysis (sci) servers is restricted to ssh login
from hosts inside the RAL firewall, so access from outside needs to be
achieved via one of the [login servers]({{< ref "login-servers" >}}).

Server name  |  Virtual/Physical (OperatingSystem)  |  Processor model  |  CPU Cores  |  RAM (GB)  |  /tmp (GB)  
---|---|---|---|---|---  
sci1.jasmin.ac.uk  |  V (CentOS7)  |  Xeon(R) Silver 4114 CPU @ 2.20GHz  |  8  |  16  |  NA  
sci2.jasmin.ac.uk  |  V (CentOS7)  |  Xeon(R) E5-2630 @ 2.20GHz  |  8  |  16  |  NA  
sci3.jasmin.ac.uk  |  P (CentOS7), **Note 1** |  AMD EPYC 7402  |  48  |  1000|  -  
sci4.jasmin.ac.uk  |  V (CentOS7)  |  Xeon E5-2660 @ 2.20GHz  |  8  |  32  |NA  
sci5.jasmin.ac.uk  |  V (CentOS7)  |  Intel(R) Xeon(R) CPU E5-2630 v4 @2.20GHz  |  8  |  32  |  NA  
sci6.jasmin.ac.uk  |  P (CentOS7), **Note 1** |  AMD EPYC 7402  |  48  |  1000|  -  
sci8.jasmin.ac.uk  |  P (CentOS7), **Note 1** |  Intel(R) Xeon(R) Gold 5118CPU @ 2.30GHz  |  24  |  383  |  -  
|  |  |  |  |  
  
**Note 1:** `sci[3,6,8].jasmin.ac.uk ` are physical servers with IP addresses
on a private internal network, so outbound internet access (via NAT) is only
for HTTP(S). This means that outbound SSH will not work (to hosts outside of
JASMIN) on these particular machines e.g. pull/clone from **Github** remote
repositories will **NOT work on these particular machines and the following
error message is triggered:** `fatal: Could not read from remote repository`.

**Note 2** : The local /tmp of the virtual VMs is not available (NA) for users
as this is used by the VM system

**Note 3:** A new monitoring utility " **Arbiter** " was implemented across
all Sci machines to control CPU and memory usage. This utility "Arbiter"
records the activity on the node, automatically sets limits on the resources
available to each user, and notifies JASMIN admin when resources quota are
changed. From the user's perspective, his/her process will be capped from
using any extra resources and the process can be slowed or run out of memory.

**Note 4:** **Users are not permitted to execute commands which require
administrative privileges.** This applies to all hosts in the managed part of
JASMIN where users have SSH login access (for example `login`, `nx-login`,
`sci`, `xfer` and `hpxfer` machines). In other words, the **use of`su` or
`sudo` is not permitted**. Please be careful when typing commands,
particularly if you have multiple terminal windows open on your own computer,
that you do not accidentally attempt `sudo`on a JASMIN machine: expect some
follow-up from the JASMIN team if you do!

Further information on using the software provided on JASMIN [can be found
here]({{< ref "software-overview" >}}).

# Purpose

Scientific analysis servers are designed for interactive and ad-hoc analysis
of data in group workspaces, the CEDA archives, and users' home directories.
**For long-running and resource-intensive jobs,** users are required to **use
the LOTUS** cluster which offers better I/O performance, parallelism, and
scheduling.

The following guide should be considered when using the scientific analysis
servers:

  * Be aware of resources available at the time before your process starts and choose the scientific server that is suitable ( check the average load on the scientific server from the message of the day on login server for example or using any of Linux monitoring command: `top`, `free -h` )
  * **Execution/processing time should be less than 1 hour** ;
  * **Serial jobs only**
  * High memory jobs should be executed on the high memory scientific servers with 1000 GB of RAM sci[3,6].jasmin.ac.uk (see above Table )
  * Monitor your process on a scientific server using `top` or `ps` Linux command 
  * Report if there is a user's process affecting the performance of a scientific server 

# Software installed

Each analysis server has the following features:

  * Default Redhat Enterprise Linux development environment.
  * The software packages that make up the [JASMIN Analysis Platform]({{< ref "software-overview#common-software" >}}) are all installed - providing commonly-used open-source analysis tools. These packages include NCO, CDO, Python2.7 (with netCDF4, matplotlib, numpy etc.,) and R.
  * Access to proprietary tools, e.g. IDL and Intel Fortran, through the Module System.
  * Ability to run X11/X-Windows applications (use the [NX graphical desktop service]({{< ref "graphical-linux-desktop-access-using-nx" >}}) to view X11 graphics output efficiently on your remote machine).

{{< alert type="danger" >}}
Users are **not permitted to execute commands which require
administrative privileges.** This applies to all hosts in the managed part of
JASMIN where users have SSH login access (for example `login`, `nx-login`,
`sci`, `xfer` and `hpxfer` machines). In other words, the **use of`su` or
`sudo` is not permitted**. Please be careful when typing commands,
particularly if you have multiple terminal windows open on your own computer,
that you do not accidentally attempt `sudo`on a JASMIN machine: expect some
follow-up from the JASMIN team if you do!
{{< /alert >}}

# Access to storage

Each analysis server has:

  * Access to the LOTUS /work/scratch-pw* and /work/scratch-nopw volumes.
  * Read access to the [CEDA Archives]({{< ref "ceda-archive" >}}) according to user permissions.
  * Read/Write access to Group Workspaces according to user permissions.
