---
aliases: /article/192-transfer-servers
date: 2021-06-28 16:14:02
description: Transfer servers
slug: transfer-servers
tags: ['transfer', 'xfer-sp']
title: Transfer servers
---

This article lists the JASMIN data transfer servers and provides links to how
they can be used.

JASMIN provides specific servers for managing data transfers. These are:

Server  |  Purpose  |  Access requirements  |  Further information  
---|---|---|---  
`xfer1.jasmin.ac.uk` |  Virtual machine for general purpose data transfers.  |`jasmin-login` |  Visible on optical network connections from `k9.leeds.ac.uk` and some Met Office hosts.
`xfer2.jasmin.ac.uk` |  Virtual machine for general purpose data transfers.  |`jasmin-login` |  
`xfer3.jasmin.ac.uk` |  As per `xfer[12]`, but with config like `login2`for enabling access from IP addresses without fwd/rev DNS lookup.  |  `jasmin-login` AND `xfer-sp` |  Apply for additional access role access [here](https://accounts.jasmin.ac.uk/services/additional_services/xfer-sp).  See below for further specifics.  
`hpxfer1.jasmin.ac.uk` |  Physical machine for high-performance data transfers.  |  `jasmin-login` AND `hpxfer`  IP address of client  |  Tuned for UK & European network paths. Apply for additional access role access[here](https://accounts.jasmin.ac.uk/services/additional_services/hpxfer)  
`hpxfer2.jasmin.ac.uk` |  Physical machine for high-performance data transfers.  |  `jasmin-login` AND `hpxfer`. IP address of client  |  Tuned for long (intercontinental) network paths (e.g. UK - Australia). Apply for additional access role access [here](https://accounts.jasmin.ac.uk/services/additional_services/hpxfer)
`gridftp1.jasmin.ac.uk` |  Physical machine for high-performance GridFTP transfers.  |  `jasmin-login` AND `hpxfer`  IP address of client  |  No SSH login access. Apply for additional access role access [here](https://accounts.jasmin.ac.uk/services/additional_services/hpxfer) Acts as Globus Online endpoint " [JASMIN GridFTP Server](https://www.globus.org/app/endpoints/4cc8c764-0bc1-11e6-a740-22000bf2d559/overview)"  
{.table .table-striped}

Please see further articles in the [Data Transfer category]({{< ref "data-transfer-overview" >}}) for details on managing your data transfers.

The standard transfer servers provide a basic and functional service for
moving small amounts of data over relatively short distances. However, the
high-performance data transfer servers shown above are also available for
those with particular requirements. Users with login accounts can [apply for
access to use the high-performance servers]({{< ref "hpxfer-access-role" >}}).

{{<alert type="info" >}}
Please make sure you use the dedicated transfer servers and not the scientific
analysis or login servers for any significant data transfers. The transfer servers have been configured to achieve the best transfer rates and will perform significantly better than other servers on jasmin, while maintaining the performance of analysis servers for interactive use by other users.
{{</alert>}}

### Special transfer machine `xfer3.jasmin.ac.uk`

This machine has been set up to cater for those whose network configuration
does not enable them to connect to xfer1 and xfer2 (for example because of a
lack of fwd/rev DNS lookup). A different set of access rules apply, which
enables users to access this machine but a side effect of these additional
rules is that **repeated attempts to access the machine via SSH-based
processes can result in being "locked out"**. This may happen when attempting
the transfer of several small files in quick succession with separate SSH
connections for each. The "xfer-sp" access group is therefore a way of
ensuring that the users accessing this machine know to be aware of this issue
and can have their access to this machine denied if found to be causing a
problem for the machine's operation for other users.

{{<alert type="danger" >}}
Users are **not permitted to execute commands which require
administrative privileges.** This applies to all hosts in the managed part of
JASMIN where users have SSH login access (for example `login`, `nx-login`,
`sci`, `xfer` and `hpxfer` machines). In other words, the **use of`su` or
`sudo` is not permitted**. Please be careful when typing commands,
particularly if you have multiple terminal windows open on your own computer,
that you do not accidentally attempt `sudo`on a JASMIN machine: expect some
follow-up from the JASMIN team if you do!
{{</alert>}}

