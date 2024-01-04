---
aliases: /article/4891-lsf-to-slurm-quick-reference
date: 2022-10-11 15:15:57
description: Slurm quick reference
slug: lsf-to-slurm-quick-reference
tags:
- scancel
- sbatch
- squeue
- cancel
- kill
- lotus
- spec
- specify
- job
- submission
- submit
- batch
- cluster
- bsub
- bqueues
- bjobs
- bkill
- bmod
title: Slurm quick reference
---

This article shows the Slurm commands and their equivalent to the LSF
scheduler (LSF was replaced by Slurm in September 2020): [this webinar](https://www.ceda.ac.uk/events/transitioning-to-slurm-webinar) gave details of the transition.

## The Slurm Scheduler

[Slurm](https://slurm.schedmd.com/) is the job scheduler deployed on JASMIN. It
allows users to submit, monitor, and control jobs on the LOTUS (cpu) and ORCHID (gpu) clusters.

**Table 1** Essential LSF/SLURM commands

**LSF** |  **Slurm** |  **Description**  
---|---|---  
bsub < _script_file_ |  sbatch _script_file_ |  Submit a job script to the scheduler  
bqueues  |  sinfo  |  Show available scheduling queues  
bjobs  |  squeue -u _\<username\>_ |  List user's pending and running jobs  
bsub -n 1 -q test -Is /bin/bash |  srun -n 1 -p test --pty /bin/bash  | Request an interactive session on LOTUS
{.table .table-striped}
  
**Table 2** Job specification

**LSF** |  **Slurm** |  **Description**  
---|---|---  
#BSUB  |  #SBATCH  |  Scheduler directive  
-q _queue_name_ |  \--partition=_queue_name or_ -p _queue_name_ |  Specify the scheduling queue   
-W _hh:mm:ss_ |  \--time=_hh:mm:ss_ or -t _hh:mm:ss_  |  Set the maximum runtime limit  
-We _hh:mm:ss_ |  \--time-min=_hh:mm:ss_  |  Set an estimated runtime  
-J _job_name_ |  \--job-name=_jobname_  |  Specify a name for the job  
-o _filename_, -e _filename_  |  \--output=_filename_ or  -o filename,  \--error=_filename_ or -e _filename_. The default file name is "slurm-%j.out", where "%j"is replaced by the job ID | Standard job output and error output. Default append.
-oo/-eo _filename_  | **For job arrays** , the default file name is "slurm-%A_%a.out", "%A" is replaced by the job ID and "%a" with the array index. 
&#xfeff; | \--open-mode=append\|truncate  |  Write mode for error/output files .
%J |  %j  | Job ID for -oo/eo filename
%I |  %a | Job array index  
-R "rusage[mem= _XXX_ ]" |  \--mem=_XXX_ |  Memory XXX is required for the job. Default units are megabytes  
-J _job_name_ [index_list]  |  \--array= _index_  (e.g. --array=1-10) |  specify a job array  
-J _job_name_ [index_list]% _number-of-simultaneous-jobs_ |  \--array=index% _ArrayTaskThrottle_  _e.g._ \--array _=1-15%4_ will limit the number of simultaneously running tasks from this job array to 4 |  A maximum number of simultaneously running tasks from the job array may be specified using a "%" separator.  
-cwd directory  |  -D, --chdir=<directory> |  Set the working directory of the batch script to < _directory >_ before it is executed.   
-x  |  \--exclusive  |  Exclusive execution mode   
-w '_dependency_expression_'  |  \--dependency= _\<dependency_list\>_ |  Defer the start of this job until the specified dependencies have been satisfied completed   
-n _number-of-cores_ |  \--ntasks=_number-of-cores or -n_ _number-of-cores_ |  Number of CPU cores   
-m <host-group-name> |  \--constraint="_\< host-group-name\>_"  |  To select a node with a specific processor model   
{.table .table-striped}

**Table 3** Job control commands

**LSF** |  **Slurm** |  **Description**  
---|---|---  
bkill _\<jobid\>_ |  scancel _\<jobid\>_ |  Kill a job  
bjobs -l _\<jobid\>_ |  scontrol show job _\<jobid\>_ |  Show details job information  
bmod _\<jobid\>_ |  scontrol update job _\<jobid\>_ |  Modify a pending job  
bkill 0  |  scancel --user=_\<username\>_ |  Kill all jobs owned by a user
{.table .table-striped}
  
**Table 4** Job environment variables

**LSF** |  **Slurm** |  **Description**  
---|---|---  
$LSB_JOBID  |  $SLURM_JOBID  |  Job identifier number  
$LSB_JOBID  |  $SLURM_ARRAY_JOB_ID  |  Job Array  
$LSB_JOBINDEX  |  $SLURM_ARRAY_TASK_ID  |  Job array index  
$LSB_JOBINDEX_END  |  $SLURM_ARRAY_TASK_MAX  |  Last index number within a job array  
$LSB_MAX_NUM_PROCESSORS  |  $SLURM_NTASKS  |  Number of processors allocated  
{.table .table-striped}
