---
aliases: /article/4732-share-software-envs
date: 2019-10-28 14:28:17
description: Sharing software environments
slug: share-software-envs
title: Sharing software environments
---

This article explains how you can share software environments with other users
on JASMIN.

## What is a software environment?

A software environment is typically a collection of files and directories
associated with a set of environment variables that allows a given session to
access them. In the context of JASMIN, there are a number of Python/other
environments already available on the system. See the [Jaspy page]({{< ref
"jaspy-envs" >}}) for examples of these.

## Creating software environments on JASMIN

In some cases, JASMIN users will need to create their own software
environments because the existing environments do not include all the packages
that they require. See the [virtual environments page]({{< ref "python-virtual-environments" >}}) for details on creating your own Python
environments.

## Tips on sharing software environments on JASMIN

If you need to create your own environment it is important to be aware of
which file system you are working on:
- SOF (e.g. `/gws/nopw/j04/*`): does not perform well with small files at present.
- SSD (e.g. `$HOME` and `/gws/smf/j04/*`): performs much better with small files.

If you are building an environment for your use only then it makes sense to
create it under your $HOME directory.

If you need to share an environment with other JASMIN users you can:
- Request a "small files" Group Workspace (GWS).
- Install the software environment within the "small files" GWS.
- Then all users with access to that GWS will be able to access the environment.


