---
aliases: /article/203-managing-a-gws
date: 2023-01-10 14:42:33
description: Managing a GWS
slug: managing-a-gws
title: Managing a GWS
---

This article explains the responsibilities of the Group Workspace (GWS)
manager.

## Role of the GWS Manager

When a GWS is created it is important that the designated GWS Manager
understands the responsibilities associated with the role. The GWS Manager has
a duty to:

  * Ensure that GWS is being used appropriately: this may include enforcement of limits on particular users.
  * Advertise the URL for requesting access to the GWS.
  * Respond to e-mail authorisation requests from CEDA.
  * Manage disk and tape effectively: specifically the use of the [Elastic Tape system]({{< ref "secondary-copy-using-elastic-tape" >}}) to back-up or migrate data.
  * Communicate [GWS etiquette]({{< ref "gws-etiquette" >}}) to the project scientists.
  * Manage additional services such as [sharing of GWS data via HTTP server]({{< ref "share-gws-data-via-http" >}}).
  * Manage the closing down of the GWS effectively: all GWSs have a termination date and data may be lost if not managed effectively.
  * Communicate any issues to the CEDA Helpdesk.

## Managing users

###  Authorising access to the GWS

When your GWS has been set up, users can submit requests for access to the GWS
via the JASMIN accounts portal: the new GWS will appear in the list of [JASMIN
Services](https://accounts.jasmin.ac.uk/account/login/?next=/services/group_workspaces/).
An access request from a user will trigger an e-mail to you that asks you to
approve (or refuse) the request. The e-mail will include details of the user
and their intended use of the resource. As GWS manager, **you** are now
responsible for approving these requests (this is a change from the previous
situation where you confirmed your approval to the CEDA helpdesk who then
actioned the approval). Now the approval is instant.

IMPORTANT: in order for this approval process to work, the GWS manager's own
account needs to have been migrated to the JASMIN accounts portal.

[Migrate your
account](https://accounts.jasmin.ac.uk/account/ceda_claim/confirm/)

### File system permissions and groups

File system access to a GWS is managed using a Unix group that begins with
"gws_". You should apply for access yourself and you may wish to set up a
directory structure as recommended in the [GWS introductory article]({{< ref
"introduction-to-group-workspaces" >}}).

A list of the user IDs that have access to a given GWS can be found by using
the "getent group" command and piping it through "grep" to select only your
GWS. For example:

```
getent group | grep gws_cedaproc<br>gws_cedaproc:*:26015:fbloggs,jdoe
```    	

You can lookup a specific user ID with the following:

```
getent passwd | grep fbloggs
fbloggs:*:29775:26030:Fred Bloggs:/home/users/fbloggs:/bin/bash
```

### Maintaining group permissions throughout the GWS

In order to maintain the group permissions throughout the GWS the highest
level directory has the "sticky bit" set. This means that the default group
for all files and directories created within the GWS will be the relevant
"gws_*" access group. This is particularly useful to enable data within the
GWS to be shared amongst collaborators. If users have a specific need to
modify the group permissions they can do so using "chgrp" command.

###  Making directory contents writable by other members of the GWS

If a user wishes to make their files/directories writable by others in the GWS
they can follow the procedure here using the "umask" command:

Make a directory (and set it the permission so that the group can read/write
to it):

```command
mkdir --mode=u+rwx,g+rws,o-rwx testdir
ls -l testdir
drwxrws--- 2 jdoe gws_cedaproc 4096 Jan 26 14:36 testdir
```    

Check the umask:

```command
umask
0022
```    

Modify the "umask" so that any new file or directory that you create will be
writable anyone with the group permission:

```command
umask 002
touch testdir/newfile
ls -l testdir
-rw-rw-r-- 1 jdoe gws_cedaproc 0 Jan 26 14:39 newfile
```

### Quota, resource allocation and GWS lifetime

The overall usage of a GWS can be determined with the `df` (SOF) or `pan_df`
(PFS) command:

```command
pan_df -H /gws/pw/j07/workshop/
Filesystem             				Size   Used  Avail Use% Mounted on
panfs://panmanager03.jc.rl.ac.uk/gws/pw/j07     2.6T    16G   2.6T   1% /gws/pw/j07/workshop/

$ df -H  /gws/nopw/j04/ncas_generic
Filesystem                                      Size   Used  Avail Use% Mounted on
quobyte@sds.jc.rl.ac.uk/gws_ncas_generic        83T    80T   3.4T  96% /gws/nopw/j04/ncas_generic
```

For PFS (`/gws/pw/j07`), the raw capacity of the GWS is 2.6TB (measured in TB,
defined using powers of 10), but to obtain space available to users this
should be divided by roughly 1.3, resulting in around 2TB of free space. Of
this, 16GB is currently in use. The factor of 1.3 can depend on the number of
small files stored in the GWS because lots of small files take up more space
than expected. For SOF, the value reported by `df` is the usable size.

A summary of specific sections of a GWS can be determined using `pan_du -sh \<di\r>` (PFS), and `du -sh --si --apparent-size \<dir\>` (SOF). Set the
`--apparent-size` flag to get an accurate size.

There is also a live view of GWSs and the available space left on the [JASMIN Dashboard](https://mon.jasmin.ac.uk). The “JASMIN Storage” tab shows many
JASMIN storage volumes with information about current usage.

You can use the `find` command together with `-atime` or `-mtime` to locate
files accessed or modified more than a certain length of time ago. For
example, to find files which were accessed more than 1 year ago:

```command
find /gws/nopw/j04/upscale/cache -type f -atime +365
```

However, the JASMIN team runs a fortnightly check of the contents of all GWSs, so please don't run large `find` jobs yourself, as this will be duplicating something already run in the background. As a GWS Manager
you will receive e-mails summarising the usage and contents of the GWS. If you
wish for additional directories to be scanned and summarised please add these
to the [GWS scanner configuration]({{< ref "gws-scanner" >}}).

The typical lifetime of a GWS is 3 years. All GWS managers are expected to
actively manage the space during its lifetime and plan for the eventual
reclamation of the space by deleting and migrating data to other locations.
Typically data might be written to Elastic Tape (see below) and some final
outputs would be curated in the CEDA Archive. In the latter case please note
that you should discuss the requirements with the CEDA Archive team via the
[CEDA Helpdesk](mailto:support@ceda.ac.uk?subject=Archiving data at CEDA).

### Migrating data to tape

Proactive data management is an important part of providing an effective GWS.
We recommend that the GWS Manager discusses use of the space with the project
team to ensure that the use of disk and tape are being optimised. This may
involve use of the [Elastic Tape system]({{< ref "secondary-copy-using-elastic-tape" >}}) 
for backup or data migration (from disk to tape).

### Requesting a change to the GWS size

Although it is helpful to provide the best estimate of required allocation at
the time of initially requesting the GWS, a GWS Manager may request a change
in size (increase or decrease) of the GWS during its lifetime. We would
positively encourage you to be honest about your requirements so that others
can make use of this expensive resource if you are not using it until later in
your project, or if you no longer require all the space you originally
requested.

Requests for an increase in GWS size will be considered by the Consortium
Manager with responsibility for managing an overall allocation to that
particular scientific community. See 
[Requesting Resources]({{< ref "requesting-resources" >}}). Depending on available resources and competing
demand, it may not always be possible to increase the allocation, and you may
be asked to move data to Elastic Tape to free up disk space.

## Security

User account security is very important in a multi-user environment such as
JASMIN. As a GWS Manager you have a responsibility to users of your GWS but
also to all other GWS users in helping to maintain a safe and secure system in
which productive scientific work can be done. There is a strict policy of one-
user-one-key, and on no account must any user make use of the SSH key of
another user to gain access to any part of the JASMIN infrastructure. Private
keys MUST be protected by a strong passphrase. Please encourage adherence to
these rules by users of your GWS. Any infringements may be dealt with swiftly
by removal of user access. No offensive, obscene or otherwise unauthorised
data may be stored in the GWS or anywhere else within JASMIN. Users should not
store any data of a personal or sensitive nature in the GWS.

{{< alert type="danger" >}}
Do not set, or allow your users to set, open permissions on files or directories.
By this we mean permissions where data are "world-writable" by anyone, for example

`-rw-rw-rw-` for a file, or
`drwxrwxrwx` for a directory. **<< DON'T USE THESE!!**

We provide a UNIX a group corresponding to each group workspace, which all members of that GWS belong to: this enables sharing within the group if you set permissions appropriately using that group. If you are unsure about setting permissions, please ask the helpdesk.
{{< /alert >}}

## Keeping informed

Please maintain contact throughout the life of the GWS via the following
channels:

  * Using the [JASMIN dashboard](https://mon.jasmin.ac.uk) to check on the status of your GWS (used versus available space).
  * Email alerts from the system when the GWS reaches >83% full
  * Email from the CEDA/JASMIN team
  * News articles on the CEDA or JASMIN websites and by monitoring CEDA social media feeds which may be used to post messages regarding system status or security. 
    * [CEDA Website](http://www.ceda.ac.uk/)
    * [CEDA News RSS feed](http://www.ceda.ac.uk/blog/feeds/rss/)
    * [CEDA on Twitter](https://twitter.com/cedanews)

If you are aware that a user who has access to your GWS leaves your project
or, for whatever reason, no longer needs to be a member of the GWS, please let
the [JASMIN Helpdesk](mailto:support@jasmin.ac.uk) know either by email or via
the beacon, lower right on this page. Arrangements may need to be made to
transfer the ownership of files and/or directories to another member of the
GWS to ensure continued access to the data.
