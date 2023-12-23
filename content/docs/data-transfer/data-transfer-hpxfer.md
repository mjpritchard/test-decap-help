---
aliases: /article/4414-data-transfer-hpxfer
date: 2021-02-17 08:52:15
description: 'Data Transfer: high-performance data transfer access'
slug: data-transfer-hpxfer
title: 'Data Transfer: high-performance data transfer access'
---

This article explains about access to high-performance data transfer services.

## Applying for access

Some data transfer services are hosted in the [JASMIN Data Transfer Zone]({{<
ref "jasmin-external-connections" >}}) for increased performance. However, to
maintain security in this zone, access is controlled via an additional access
group "hpxfer". If you have a login account already, you can apply here for
this additional role:

[Apply for hpxfer
access](https://accounts.jasmin.ac.uk/account/login/?next=/services/additional_services/hpxfer/)

## Additional information required

If you will be connecting from your home institution directly via ssh or ssh-
based gridftp to one of the servers in the JASMIN Data Transfer Zone, the
specific IP address of your machine will need to be added to an allowed list.
Please supply this as part of the application process above.

However, this should not be necessary if you are accessing the server from a
remote server which is already allowed. Similarly, if you are using Globus
Online, relevant IP addresses have already been allowed.

**Inward** pulls of data (to JASMIN) are possible by logging in to
`hpxfer[1,2].jasmin.ac.uk` **via the login servers** and pulling data from
external data sources. So if you're not sure what IP address to use when
applying for access above, it is OK to quote the IP address of
`login1.jasmin.ac.uk`, i.e. `130.246.130.28` as a "dummy" value if you will
only be accessing them via this route, and not directly from outside.
