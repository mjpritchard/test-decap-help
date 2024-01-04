---
aliases: /article/191-login-servers
date: 2022-06-08 12:57:52
description: Login servers
slug: login-servers
tags:
- xfer-sp
- xfer3
- login2
- login1
- xfer1
- xfer2
title: Login servers
---

## Available login servers

There are three login servers available to access resources within JASMIN.
Users with the `jasmin-login` access role can access the following servers via
SSH:

Login server name | details |
|---|---|  
| `login1.jasmin.ac.uk`  | | 
| `login2.jasmin.ac.uk`  | Contingency, see notes below  |
| `login3.jasmin.ac.uk`  |  |
| `login4.jasmin.ac.uk`  | |
{.table .table-striped}
  
See also [How to login]({{< ref path="docs/getting-started/login" >}}) and other articles in the [Getting started]({{< ref "getting-started" >}}) category.

See also [NoMachine NX service]({{< ref "graphical-linux-desktop-access-using-nx" >}}) which provides login to a graphical Linux desktop, rather than a
single terminal window.

## Features of login servers

Login servers have minimal resources and software installed. They provide:

  * Access to your home directory (`/home/users/<username>`).
  * Access via SSH to other hosts within JASMIN (inside the RAL firewall)
  * No analysis software is installed on the login servers.
  * No access to group workspaces or other volumes.

## "Contingency" login servers

There are [requirements on your local network]({{< ref "check-network-details"
>}}) which apply to accessing the login servers **and** the [transfer
servers]({{< ref "transfer-servers" >}}) via SSH. If you cannot meet these
requirements, even after discussion with your local network admin team, a
contingency route is provided in the form of login server
`login2.jasmin.ac.uk`

However, you will be limited in what you can access within JASMIN from this
server. Specifically:

  * You will not be able to access the transfer servers `xfer[1,2].jasmin.ac.uk` via SSH directly from an external host.  

  * You can access these via SSH from `login2`, but can then only initiate an inward pull of data from an external SSH server, if available at your institution. You cannot push data directly to `xfer[1,2].jasmin.ac.uk` via SSH from outside in this case.
  * Instead, an alternative transfer server `xfer3.jasmin.ac.uk` is provided with equivalent configuration to `login2`. This should provide what you need for direct SSH transfers from outside, but you will need the additional `"xfer-sp"` access role in in this case: see [here for further details]({{< ref "transfer-servers" >}}).

# How to use the login servers

For full details of how to log in, including making onward connections to
other machines, please see the article ["How to login"]({{< ref path="docs/getting-started/login" >}}).

{{<alert type="danger">}}
Users are **not permitted to execute commands which require
administrative privileges**. This applies to all hosts in the managed part of
JASMIN where users have SSH login access (for example `login`, `nx-login`,
`sci`, `xfer` and `hpxfer` machines).


In other words, the **use of`su` or
`sudo` is not permitted**.

Please be careful when typing commands,
particularly if you have multiple terminal windows open on your own computer,
that you do not accidentally attempt `sudo`on a JASMIN machine: expect some
follow-up from the JASMIN team if you do!
{{</alert>}}
