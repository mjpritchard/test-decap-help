---
title: Important use of JASMIN storage - ALL USERS PLEASE READ
date: 2018-11-15 16:55:00+00:00
tags: ['news']
aliases: ['/blog/important-use-of-jasmin-storage-all-users-please-read']
thumbnail: 
icon: fas circle-info
---
As we proceed with providing storage space to Group Workspaces on JASMIN’s new Scale-Out File System (SOF) storage, it is important that users understand some critical differences between this storage and the Panasas storage used elsewhere in the system.


  
DOES THIS AFFECT ME?


  
1) If you use a group workspace with a path  
/group\_workspaces/jasmin4/\*  
or  
/gws/nopw/j04/\*


  
Then: YES: this directly affects you NOW, so please read on.


  
2) If you use a group workspace with a path  
/group\_workspaces/cems2/\*  
or  
/group\_workspaces/jasmin2/\*


  
Then: PROBABLY: There is a good chance that your GWS is earmarked for migration to this new storage over the next few weeks (your GWS manager will be contacted if so). So please read on anyway, as this is likely to affect you in the near future.


  
ISSUE  
As currently configured, the new SOF storage does not support parallel writes.  
Attempts to write to the same file from different concurrent processes will fail with wider consequences  
These failures can cause storage volumes to become stuck, leaving the affected files unable to be closed and causing the volume and often the affected host to become locked, requiring a reboot to rectify the situation.  
It is possible for certain storage volumes to be configured to allow this capability, but with significant costs.


  
ACTION  
Please can ALL users check their code, scripts, and particularly any workflow logic used to create logs and output files, to avoid the situation where a file is open for writing by more than 1 process at the same time. This includes use of the MPI-IO library (but please ask for advice in this case. Some uses are ok)  
A common cause of this is writing log files for multiple jobs run on LOTUS to the same file.  
To avoid this the template “%J” can be used to help create per-job log file names, where %J is replaced by the JobID number. But if you are using job arrays then you must also use “%I” to refer to the individual job array element number in the log or output file name.


  
In more detail:  
The log file names are specified using the -o and -e options (given on the bsub command line or in #BSUB lines in the script), for job standard output and standard error respectively.


  
a) Multiple distinct jobs might use the same -o option -- so the user should include %J unless they are confident that they are using a separate output file for each job. [this also applies to job arrays]  
Eg. “bsub -o mylogfile.o -e myerrfile.e ” becomes “bsub -o mylogfile.%J.o -e myerrfile.%J.e” where %J is replaced by the LSF jobID number.


  
b) Jobs within a job array will by definition all be using the same -o option, so the user should certainly include %I if using a job array.  
E.g. bsub -o mylogfile.%J.%I.o


  
c) both a) and b) apply when using -e


  
d) see job submission examples in <https://help.jasmin.ac.uk/article/113-submit-jobs>


  
But please also be aware of this issue WHEREVER you are writing to output files on JASMIN, whether using LOTUS or one of the SCI machines, and whether or not your storage is on one of the affected volumes (many users belong to multiple Group Workspaces).


  
Thanks in advance for your cooperation


  
JASMIN Team

