---
aliases: /article/5037-data-transfer-tools-rclone
description: 'A "Swiss army knife" tool for data transfers'
slug: rclone
title: 'rclone'
tags:
- cloud
- s3
- sync
---

This article provides information about the rclone data transfer tool. In
particular:

- what is rclone?
- installing rclone for yourself on JASMIN.
- configuring rclone
- Dos and Don'ts

## What is rclone?

rclone is a command-line utility which enables access to lots of different
storage systems including object stores and cloud-based storage. It can also
move data between directories act as an SFTP client so could be used to access
files on JASMIN.

It is very well [documented](https://rclone.org/) already, so rather than
repeat that information here, this article highlights aspects relevant to its
use on JASMIN.

Further information will follow in due course as our experience with this tool
develops.

## Installing rclone for yourself on JASMIN

First off, **do not attempt to follow the documented instructions for
installing on Linux**. As a regular user, **you do not have root/administrator
permission and are not permitted to run scripts using sudo**. Normally most
utilities are already installed for you on JASMIN, but in this case you need
to adapt the documented instructions so that you can safely install this in
your OWN home directory. [That may change in the future if this tool proves
useful].

The recommended procedure for installation on JASMIN is as follows:

Fetch and unpack the Linux binary distribution: (in your home directory on an
**xfer** server)

{{<command>}}
curl -O https://downloads.rclone.org/rclone-current-linux-amd64.zip
unzip rclone-current-linux-amd64.zip
cd rclone-*-linux-amd64
{{</command>}}

Next, move the `rclone` executable to your own `bin` directory. You may need
to create that directory if it does not exist already, and add it to your
`PATH` environment variable in your `~/.bash_profile` file.

{{<command shell="bash">}}
## only need these if these aren't in place already in your own setup:
mkdir ~/bin # comment here

## add this to your PATH (add to your ~/.bash_profile to make this permanent)
export PATH="~/bin:$PATH"

## move the rclone executable
mv rclone ~/bin/

## make the permissions on the file executable by you
chmod 700 ~/bin/rclone
{{</command>}}

Note that you will not have installed the man pages, so these will not be
available: please consult the online documentation instead.

## Configuring rclone

Configuring rclone is covered in the rclone documentation. Essentially you
need to configure a **"remote"** representing each storage system you want to
interact with. You can then use rclone to manage data between those "remotes".

## Dos and Don'ts

- Please **DO NOT use the following features on JASMIN** (at least until further notice). Some of these features look useful, but more work is needed to understand if/how they can be used safely on JASMIN without causing problems. 
  - `rclone mount` (mounting a remote as a filesystem) - **DO NOT USE**
  - `rclone rcd` (remote control daemon) - **DO NOT USE**
  - `rclone serve`(serve remote over a protocol) - **DO NOT USE**
- You should safely be able to use the following, between remotes that you have configured: 
  - `rclone copy`
  - `rclone sync`
  - `rclone lsd`
  - `rclone ls`
  - `..(other basic commands)`

Help on a particular command is found using

{{<command>}}
rclone <command> --help
{{</command>}}

Further examples of useful ways of using rclone on JASMIN will follow...
