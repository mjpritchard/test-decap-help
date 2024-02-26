---
aliases: /article/219-data-transfer-overview
description: Overview of data transfer
slug: data-transfer-overview
title: Data transfer overview
---

This article introduces the topic of data transfer to/from JASMIN.

## Introduction to Data Transfer on JASMIN

As a JASMIN user you are very likely to be involved in data transfer. You
might need to copy data files/directories from JASMIN to remote sites (such as
your own PC, MONSooN or ARCHER2) or bring new data on to JASMIN. These data
transfer articles explain how to use the basic [transfer tools]({{< ref "data-transfer-tools" >}}) such as `rsync` and `scp` as well as more sophisticated
methods such as GridFTP. They also cover which transfer services and servers
are available to JASMIN users.

For many users, moving small amounts of data over short distances, the basic
tools will meet their requirements. However, data transfer is a complicated
topic so we also provide articles about how you can improve your transfer
rates to make the most of the available bandwidth. We include details about
transfers over connections to specific sites (such as the Met Office). Advice
is also provided about automating and scheduling data transfers, along with
tips for different transfer workflows.

## Transfers to/from JASMIN

### 1\. Transfers initiated from JASMIN

When initiating a transfer from a transfer server on JASMIN you would usually
start by logging on to the server (via SSH). Once you are logged in you can
initiate a connection to the outside world in order to push/pull the data you
require.

### 2\. Transfers initiated from elsewhere

When initiating a transfer from elsewhere you will transfer data files to/from
a source machine (which may be inside or outside JASMIN) to the transfer
server.

### Transfer directories

You will typically transfer data to/from a Group Workspace that you have been
granted access to. If you are copying data from JASMIN you might want to copy
data from the CEDA archive (mounted on JASMIN) to a remote site. You might
also wish to copy small volumes of data to/from your $HOME directory. All of
these locations are available on the transfer servers.

### JASMIN Transfer servers

JASMIN provides specific [servers for managing data transfers]({{< ref
"transfer-servers" >}}). Please read about the different servers available for
particular data transfer needs, and about the various [data transfer
tools]({{< ref "data-transfer-tools" >}}) available.

## Improving your transfer rates

To achieve better transfer rates, for large transfers or where speed and reliability are important, you are recommended to:

- use the Globus data transfer service (recommended), or
- use the high-performance data transfer servers ({{<link "hpxfer-access-role">}}hpxfer access role required{{</link>}})