---
aliases: 
    - /article/4891-lsf-to-slurm-quick-reference
    - /docs/batch-computing/lsf-to-slurm-quick-reference/
date: 2022-10-11 15:15:57
description: An overview of Slurm commands and its environment variables
slug: slurm-quick-reference
tags:
- lotus
- orchid
- slurm
title: Slurm quick reference
---

## The Slurm Scheduler

[Slurm](https://slurm.schedmd.com/) is the job scheduler deployed on JASMIN. It
allows users to submit, monitor, and control jobs on the [LOTUS]({{< ref "lotus-overview" >}}) (CPU) and [ORCHID]({{< ref "orchid-gpu-cluster" >}}) (GPU) clusters.

## Essential Slurm commands

| **Slurm command**                  | **Description**                         |
| ---------------------------------- | --------------------------------------- |
| sbatch _script_file_               | Submit a job script to the scheduler    |
| sinfo                              | Show available scheduling queues        |
| squeue -u _\<username\>_           | List user's pending and running jobs    |
| srun -n 1 -p test \--pty /bin/bash | Request an interactive session on LOTUS |
{.table .table-striped}
  
## Job specification

<!-- Turn word wrap off to edit this table, or use a site such as https://tableconvert.com/markdown-to-markdown -->
| **Slurm parameter**                                                                                                                             | **Description**                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| #SBATCH                                                                                                                                         | Scheduler directive                                                                                                                 |
| \--partition=_queue_name_ <br> -p _queue_name_                                                                                                  | Specify the scheduling queue                                                                                                        |
| \--time=_hh:mm:ss_ or -t _hh:mm:ss_                                                                                                             | Set the maximum runtime limit                                                                                                       |
| \--time-min=_hh:mm:ss_                                                                                                                          | Set an estimated runtime                                                                                                            |
| \--job-name=_jobname_                                                                                                                           | Specify a name for the job                                                                                                          |
| \--output=_filename_ or  -o _filename_ <br> \--error=_filename_ or -e _filename_                                                                | Standard job output and error output. Default append. The default file name is `slurm-%j.out`, where `%j` is replaced by the job ID |
| \--open-mode=append\|truncate                                                                                                                   | Write mode for error/output files                                                                                                   |
| %j                                                                                                                                              | Job ID                                                                                                                              |
| %a                                                                                                                                              | Job array index                                                                                                                     |
| \--mem=_XXX_                                                                                                                                    | Memory XXX is required for the job. Default units are megabytes                                                                     |
| \--array= _index_  (e.g. \--array=1-10)                                                                                                         | Specify a job array. The default file name is `slurm-%A_%a.out`, `%A` is replaced by the job ID and `%a` with the array index.      |
| \--array=index% _ArrayTaskThrottle_  <br> (e.g. \--array=1-15%4 will limit the number of simultaneously running tasks from this job array to 4) | A maximum number of simultaneously running tasks from the job array may be specified using a `%` separator.                         |
| -D <br> \--chdir=_\<directory\>_                                                                                                                | Set the working directory of the batch script to < _directory >_ before it is executed.                                             |
| \--exclusive                                                                                                                                    | Exclusive execution mode                                                                                                            |
| \--dependency= _\<dependency_list\>_                                                                                                            | Defer the start of this job until the specified dependencies have been satisfied completed                                          |
| \--ntasks=_number-of-cores_ <br> -n _number-of-cores_                                                                                           | Number of CPU cores                                                                                                                 |
| \--constraint="_\< host-group-name\>_"                                                                                                          | To select a node with a specific processor model                                                                                    |
{.table .table-striped}

## Job control commands

| **Slurm command**               | **Description**               |
| ------------------------------- | ----------------------------- |
| scancel _\<jobid\>_             | Kill a job                    |
| scontrol show job _\<jobid\>_   | Show details job information  |
| scontrol update job _\<jobid\>_ | Modify a pending job          |
| scancel \--user=_\<username\>_  | Kill all jobs owned by a user |
{.table .table-striped}
  
## Job environment variables

| **Slurm variable**    | **Description**                      |
| --------------------- | ------------------------------------ |
| $SLURM_JOBID          | Job identifier number                |
| $SLURM_ARRAY_JOB_ID   | Job array                            |
| $SLURM_ARRAY_TASK_ID  | Job array index                      |
| $SLURM_ARRAY_TASK_MAX | Last index number within a job array |
| $SLURM_NTASKS         | Number of processors allocated       |
{.table .table-striped}
