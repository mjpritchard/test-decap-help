---
aliases: /article/176-storage
description: Access to storage
slug: storage
tags:
- quota
- backup
- scratch
- nopw
- pw
- ssd
- smf
title: Access to storage
weight: 150
---

This article provides information about JASMIN storage. It covers:

  * Home directory 
  * JASMIN disk mounts
  * Where to write data
  * How to use the temporary disk space
  * Cleaning up the work scratch and `/tmp`
  * Access to the CEDA archive
  * Tape access
  * Advice on inter-volume symlinks in JASMIN storage

**IMPORTANT:** Please see also [Understanding new JASMIN storage]({{< ref
"understanding-new-jasmin-storage" >}}) which explains more about the
different types of storage as of Phase 4.

## Home directory

Every JASMIN user is allocated a HOME directory located
at`/home/users/<user_id>`. This directory is available across most of the
interactive and batch computing resources, including the JASMIN login and
transfer servers.

Each home directory has a default **quota of 100 GB** (as of [JASMIN Phase
4](http://www.jasmin.ac.uk/phase4) \- Please note that information about how
to check your quota is still pending, due to a change of storage technology
for this area). You can find your current usage by running the following Linux
command:

    
    
    pdu -sh /home/users/<username>
    

**IMPORTANT** : You are only allowed to exceed the 100 GB quota for a very
brief period of time but if you continue to exceed the limit, you will be
unable to add any more files or run jobs and will be required to reduce your
usage.

### Backups of your home directory

Your home directory is backed up using a daily snapshot which provides a quick, **self-service** method for you to restore files or directories that have been accidentally deleted. Snapshot backups are kept for 1-2 weeks before being deleted.

#### Recovering snapshots of your home directory data

Users can access snapshots to recover files/directories that have been
accidentally deleted. These are stored in
`/home/users/.snapshot/homeusers.<snapshotid>/<username>`

The most recent backup is the one with the highest snapshot id number.

Find the ones relevant to your username with a command line this: (
`${USER}`is the environment variable containing your username, so can be
copied in this case)

    
    
    # ls -ld /home/users/.snapshot/homeusers.*/${USER}
    

Within each of these, you can look for your own username to find snapshot
directories for your data. File(s) can then be copied (by users themselves)
back from one of these directories to their original location.

    
    
    # ls -l /home/users/.snapshot/homeusers.45678/joebloggs/
    total 1170964
    -rw-r--r-- 1 joebloggs users              104857600 Jun 26  2017 100M.dat
    -rw-r--r-- 1 joebloggs users             1024000000 Feb  1  2017 1G.dat
    -rw-r--r-- 1 joebloggs users                      0 Dec 18 12:09 6181791.err
    
    # cp /home/users/.snapshot/homeusers.45678/joebloggs/100M.dat ~/100M.dat
    

**Home directories should not be used for storing large amounts of data**. See
below for guidance on where to write your data.

A snapshot backup is also provided for `/gws/smf`volumes (small allocations of
SSD storage for GWS groups to share): snapshots in this case are made hourly
and kept for 10 hours and then daily snapshots are kept for 2 weeks. These can
be retrieved in a similar manner to that shown above. In this case the
relevant directories should be found at

    
    
    /gws/smf/jNN/<gwsname>/.snapshot
    

(where `NN` = `04` or `07` depending on where the volume is located)

But **note that`/gws/smf`volumes are not subject to tape backups and, like
other group workspace volumes, are NOT backed up.**

Please note advice on inter-volume symlinks, below: these are to be avoided.

## JASMIN disk mounts

There is a common file system layout that underpins most of the JASMIN
infrastructure. However, access to different parts of the file system will
depend on where you are logged in. Table 1 outlines the key disk mounts, where
they are accessible from and the type of access (read and/or write).

**Table 1.** List of common disk mounts, types of storage and their
availability on JASMIN

Disk mount  
|  login  |  sci  |  transfer  |  LOTUS  |  Type  |  Parallel-write  
---|---|---|---|---|---|---  
/home/users  |  R/W  |  R/W  |  R/W  |  R/W  |  SSD  |  no  
/group_workspaces/jasmin2  
/gws/pw/j05  
/gws/nopw/j04 (see note 1 below)  
/gws/smf/j04, j07  |  No  
No  
No  
No  |  R/W  
R/W  
R/W  
R/W  |  R/W  
R/W  
R/W  
R/W  |  R/W  
R/W  
R/W  
R/W  |  PFS  
PFS  
SOF  
SSD  |  yes  
yes (hence "pw")  
no (hence "nopw")  
no  
/work/xfc/volX (see note 1 below)  |  No  |  R/W  |  R/W  |  R/W  |  SOF  |
no  
/work/scratch-pw [RO from 22 Nov 2022]  
/work/scratch-pw2  
/work/scratch-pw3 [new]  
/work/scratch-nopw  |  No  
No  
No  
No  |  RO  
R/W  
R/W  
R/W  
|  No  
No  
No  
No  |  RO  
R/W  
R/W  
R/W  
|  PFS  
PFS  
PFS  
SSD  |  yes  
yes  
yes  
no  
/apps/contrib  |  No  |  RO  |  No  |  RO  |  n/a  |  n/a  
/badc, /neodc (archives)  |  No  |  RO  |  RO  |  RO  |  n/a  |  n/a  
  
login = [login servers]({{< ref "login-servers" >}}): login[1-4].jasmin.ac.uk  
sci = [scientific analysis servers]({{< ref "sci-servers" >}}):
sci[1-6,8].jasmin.ac.uk  
transfer = [data transfer servers]({{< ref "transfer-servers" >}}):
xfer[1-2].jasmin.ac.uk  
LOTUS = [LOTUS batch processing cluster]({{< ref "slurm" >}}) (all cluster
nodes)  
Disks are mounted read/write (" **R/W** ") or read-only (" **RO** ").

**Note 1:** Please refer to issues related to writing small files and NetCDF3
to SOF storage [here]({{< ref "faqs-storage" >}})

## Where to write data

As indicated in table 1 there are three main disk mounts where data can be
written. Please follow these general principles when deciding where to write
your data:

  1. HOME directories (`/home/users`) are relatively small (100GB as of Phase 4) and **should NOT be used for storing large data volumes**.
  2. Group Workspaces (`/group_workspaces/*/<project>` and `/gws/nopw/*/<project`) are **usually the correct place to write your data**. Please refer to the [Group Workspace]({{< ref "short-term-project-storage" >}}) documentation for details. But please note that Group Workspaces are **NOT backed up**. 
    1. `/group_workspaces/jasmin2` volumes are parallel-write-capable storage from Phases 2 and 3 of JASMIN. Some of this storage is due for retirement by the end of 2018 with data to be migrated to new volumes on `/gws/nopw/j04`
    2. `/gws/pw/j05` volumes are parallel-write-capable storage from Phase 5 of JASMIN
    3. `/gws/nopw/j04` volumes are "Scale out Filesystem" (SOF) storage which is not parallel-write-capable. This new naming convention will be used for all new volumes and whenever existing volumes are migrated to SOF storage from now on.
  3. The "scratch" areas (`/work/scratch-pw2`, `/work/scratch-pw3 ` and `/work/scratch-nopw`) are available as a temporary file space for jobs running on [LOTUS]({{< ref "slurm" >}}) (see next section below).
  4. The (`/tmp`) directory is **not an appropriate location to write your data (see next section below).**

## How to use the temporary disk space

The scratch areas `/work/scratch-pw2`, `/work/scratch-pw3 ` and
`/work/scratch-nopw` are a temporary file space shared across the entire LOTUS
cluster and the scientific analysis servers.

These scratch areas are ideal for processes that generate _intermediate_ data
files that are consumed by other parts of the processing before being deleted.
Please remember that these volumes are resources shared between all users, so
consider other users and remember to clean up after your jobs. **** Any data
that you wish to keep should be written to a Group Workspace.

There are now 2 types of scratch storage available:

  * `/work/scratch-nopw` suitable for most users (90 TB available, introduced in [JASMIN Phase 4](http://www.jasmin.ac.uk/phase4/#scratch)) 
    * Please use this area unless you have a good reason not to. The flash-based storage has significant performance benefits particularly for operations involving lots of small files, but it is not suitable for MPI-IO operations that attempt to write in parallel to different parts of the same file. Please be aware of this if your code (perhaps inadvertently?) writes to a shared log file.
  * `/work/scratch-pw[2,3]` and for users with a specific need for storage that is capable of shared-file writes with MPI-IO (1 PB available) 
    * Please use this area ONLY if you know that your code has a parallel-write requirement.

When using the "scratch" areas, please create a sub-directory (e.g.
`/work/scratch-nopw/<username>`) and write your data there.

In contrast to the "scratch" space, the `/tmp` directories are all local
directories, one per cluster node (or interactive server). These can be used
to store _small_ volumes of temporary data for a job that only needs to be
read by the local process.

## Cleaning up the scratch and tmp directories

Please make sure that your jobs delete any files under the `/tmp`and scratch
directories when they are complete ( _especially_ if jobs have not been
completed normally!).

**IMPORTANT:** Please note that an automated cleanup script runs daily and
deletes files that are older than 28 days from the last time of being
accessed. This applies to `/work/scratch-pw2`, `/work/scratch-pw3` and
`/work/scratch-nopw`

**Data in the** `/tmp` **,**`/work/scratch-pw[2,3]` and `/work/scratch-nopw`
**directories are temporary and may be arbitrarily removed at any point once
your job has finished running. Do not use them to store important output for
any significant length of time. Any important data should be written to
a[group workspace](http://www.jasmin.ac.uk/services/group-workspaces/) so that
you do not lose it, or to your home directory if appropriate.**

The `/work/scratch-pw[2,3]` and `/work/scratch-nopw`areas are NOT available on
the xfer or login servers.

**Any temporary data files can reside in a subdirectory of your group
workspace instead of /tmp.** To do this, please add the following lines (or
similar) to your $HOME/.bashrc file:

    
    
    export TMPDIR=/group_workspaces/jasmin/<your_project>/<your_username>/tmp
    

  * # create the directory if needed

[ -d $TMPDIR ] || mkdir -p $TMPDIR

## Access to the CEDA archive

The CEDA archive is mounted read-only under `/badc` (British Atmospheric Data
Centre) and `/neodc` (NERC Earth Observation Data Centre). The archive
includes a range of data sets that are provided under varying licences. Access
to these groups is managed through standard Unix groups. Information about the
data and their access restrictions is available from the [CEDA Data
Catalogue](http://catalogue.ceda.ac.uk/). **As a JASMIN user, it is your
responsibility to ensure that you have the correct permissions to access data
from the CEDA archive.**

## Tape access

Group workspace managers also have [access to a tape library (Elastic Tape
service)]({{< ref "secondary-copy-using-elastic-tape" >}}) for making
secondary copies and managing storage between online and near-line storage.

## Number of files in a single directory

It is highly recommended that you do not exceed more than 100,000 files in a
single directory on any type of storage on JASMIN. Large numbers of files
place unnecessary load on components of the file system and can be the source
of slow performance for you and other storage volumes in the system. To count
the number of files, please note the advice in "Slow ls response" below, or
use an alternative command e.g. `find`.

## Slow 'ls' response

This can be due to a number of reasons (see above advice regarding number of
files in a single directory, and below regarding inter-volume symlinks). To
speed up the response (useful if you want to count the number of files) it
often helps to un-alias ls, e.g. by placing a backslash in front of the
command: `\ls`.

## Advice on inter-volume symlinks in JASMIN storage

We highly recommend users _not_ to use symbolic links in their home
directories to other parts of the JASMIN file systems, such as GWSs or scratch
areas. There are a number of conditions when the petabyte-scale JASMIN storage
can become unusable for all users due to these links. There is a more
technical explanation below. We would advise path substitutions using
environment variables instead.

Symlinks in users' home directories that point to other volumes (for example
group workspaces) make matters worse _when_ there are problems on the
`sci*.jasmin.ac.uk` servers and other shared machines, and/or when the
metadata servers responsible for particular storage volumes themselves become
overloaded. The simplest advice we can currently give is to **avoid** using
symlinks.

**In more detail:**

This issue is particularly apparent when `ls` is aliassed to `ls --color` (as
is the default on 99% of JASMIN systems) AND one of the colorisation options
specified is for an orphaned link. The `ls` on symlinks causes the metadata
servers at the end of the symlink to be called (to provided the `stat`
filesystem metadata), in addition to the metadata server for the home
directory. If those metadata servers at the far end are under load, or have
some other problem, the `ls` to the home directory can hang, but this also
hangs other users who may be trying to ls their own home directory (even if
theirs contains no symlinks). The situation can then escalate out of control
as more and more users try and fail.

This is already recognised as an issue particularly with the older part of our
storage estate, but especially where one or more of the volumes involved
contains large numbers of small files.

There are likely other issues at play as well, some of which may be addressed
by our current upgrade plans which involve replacing older parts of the
storage over the next few months.


