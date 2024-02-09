---
aliases: /article/3822-scheduling-automating-transfers
date: 2021-07-07 14:35:42
description: Scheduling/Automating Transfers
slug: scheduling-automating-transfers
title: Scheduling/Automating Transfers
---

This article explains how to schedule or automate data transfers. It covers:

  * Scheduling download tasks using cron and LOTUS
  * Using Globus for transfer automation [TODO]

## Overview

In many cases it can be useful to fetch data from an external source for
processing/analysis on JASMIN on a regular basis, for example "every Monday at
11:00 fetch all last week's data". It can also be helpful to distribute the
task downloading of some large datasets, or simply to be able rely on data
being pulled in from some external source to an accumulating dataset used for
periodic analysis.


##  Using Globus for transfer automation

It is easy to automate transfers using {{<link "globus-transfers-with-jasmin">}}Globus{{</link>}}. This method has the advantage that you 
do not need to remain connected or logged in to any JASMIN server for the automated transfers
to take place on your behalf, and is more efficient and reliable than the other methods described below.

Some introductory information about how to do this is available in this article
{{<link "globus-command-line-interface/#automation">}}Using the Globus command-line interface{{</link>}}
(with more to follow)
but please also refer to the comprehensive Globus documentation and their 
[automation examples](https://github.com/globus/automation-examples). You can choose whether 
to schedule/automate tasks via the Globus web interface, command-line interface, or use their Globus SDK to build
Python code that uses this functionality.

## Scheduling download tasks using cron and LOTUS

While the [cron server]({{< ref "using-cron" >}}) is provided for scheduling
tasks, **it should not be used for the work of executing those tasks itself.**
So we need a way for a task to be invoked from cron but executed where there
is lots of processing resource (i.e. LOTUS).

In the examples below, we use the `test` queue (or partition, as queues are
known in SLURM). You can use this for testing, but once you know roughly how
long your download(s) should take, you should [choose an appropriate
queue]({{< ref "slurm-queues" >}}) so that the jobs can be scheduled in a fair
way alongside other users' jobs.

### 1\. Single download script

The simple script below is used to download a single file from an external
source via HTTP using `wget`:

    
    
    #!/bin/bash 
    #SBATCH --partition=test
    #SBATCH -o %j.out 
    #SBATCH -e %j.err
    #SBATCH --time=00:30
    
    # executable 
    wget -q -O 1MB_${SLURM_JOBID}.zip http://speedtest.tele2.net/1MB.zip
    

In this example, the file is labelled with the id of the job which downloaded
it, e.g. `1MB_61117380.zip`

The same could be also achieved using `curl`, or using a Python script making
use of (for example) the `requests` library.

**A note about transfer tools:** since we are delegating the actual download
task to a LOTUS node, we are restricted to transfer tools already installed on
those nodes or available in the user's path at a location cross-mounted with
nodes in the LOTUS cluster (see Table 1 in [Access to Storage]({{< ref path="/docs/getting-started/storage" >}})), such as $HOME or a group workspace. It is not possible for
the JASMIN team to install specialist data transfer tools across the whole
cluster, so you may be limited to downloading via HTTP(S), FTP, or via tools
available via libraries in the Python environment such (which you do have
access to and can easily customise to install additional libraries using
virtual environments).

Download tools installed on LOTUS nodes include:

  * `wget`
  * `curl`
  * `ftp` (but not `lftp`)

In our simple example above, we can subit this script to LOTUS from the
command line with

    
    
    sbatch test_download.sh
    

This could be invoked on a regular basis by adding a crontab entry like this

    
    
    30 * * * * sbatch /home/users/username/test_download.sh
    

However it would be safer to wrap this in a `crontamer` command like this to
ensure one instance of the task had finished before the next started: (see
[Using cron]({{< ref "using-cron" >}}) for details)

    
    
    30 * * * * crontamer -t 2h 'sbatch /home/users/username/test_download.sh'
    

## 2\. Multi-node downloads

We could expand this example to download multiple items, perhaps 1 directory
of data for each day of a month, and have 1 element of a job array handle the
downloading of each day's data.

**A few words of warning:** Distributing download tasks as shown below can
cause unintended side-effects. Here, we're submitting an array of 10 download
jobs, each initiating a request for a 1MB file which may well happen
simultaneously. So we need to be confident that the systems and networks at
either end can cope with that. It would be all too easy to submit a task to
download several thousand large data files and cause problems for other users
of JASMIN (and other users on its host institution's network), or indeed at
the other end. Taken to the extreme, this could appear over the network as a
Distributed Denial-of-Service (DDoS) attack. As with all LOTUS tasks: start
small, test, and increase to sensible scales when you are confident it will
not cause a problem. **A limit of 10 jobs would be a sensible maximum, for one
user.**

We'll simulate this here by downloading the same external file to 10 different
output files, but you could adapt this concept for your own purposes depending
on the layout of the source and destination data.

    
    
    #!/bin/bash 
    #SBATCH --partition=test
    #SBATCH -o %A_%a.out
    #SBATCH -e %A_%a.err
    #SBATCH --time=00:30
    #SBATCH --array=1-10
    #SBATCH --time=00:30
    
    # executable 
    wget -q -O 1MB_${SLURM_ARRAY_TASK_ID}.zip http://speedtest.tele2.net/1MB.zip
    
    echo "script completed"
    

In this (perhaps contrived) example, we're setting up an array of 10 elements
and using the `SLURM_ARRAY_TASK_ID` environment variable to name the output
files (otherwise they'd all be the same). In a real-world example you could
apply your own logic to divide up files or directories matching certain
patterns to become elements of a job array.

The script could then be scheduled to be invoked at regular intervals as shown
in (1).

Some tools provide functionality for mirroring or synchronising directories,
i.e. only downloading those files in a directory which are new have been added
since the last time a task was run. These can be useful to avoid repeated
downloads of the same data.

