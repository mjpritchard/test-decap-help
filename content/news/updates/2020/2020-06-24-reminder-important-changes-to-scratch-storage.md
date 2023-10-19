---
title: Reminder - IMPORTANT Changes to Scratch Storage
date: 2020-06-24 14:21:30+00:00
tags: ['news']
aliases: ['/blog/reminder-important-changes-to-scratch-storage']
thumbnail: /img/news/2020/2020-06-24-reminder-important-changes-to-scratch-storage/jasmin_logo_500px.jpg
icon: 
---

Dear JASMIN users,


**Please note the following changes that affect the** */work/scratch*  
We have previously announced that the new scratch volume */work/scratch-pw* is available. This volume is on PFS (parallel file system) storage with a total capacity of 1 Petabyte, but has automated processes in place to “police” usage. The old volume, */work/scratch* will be available for READ access only from this **Friday 26th June until 31st July.** Please do not run batch jobs that write to */work/scratch* as your job will fail.


**Note:** */work/scratch* will be retired after the 31st July.


As always with scratch storage, any important data should be moved away to other storage if it is to be kept for any length of time. The primary purpose of scratch storage is for intermediate storage for batch processing jobs on LOTUS. To “police” this, and to preserve the availability of scratch space for all LOTUS users, automated processes will be run at weekly intervals to purge all data older than 28 days.  
   
We are also taking this opportunity to remind users of the naming convention ‘pw’ and ‘nopw’ to help distinguish between “parallel write” (pw) and “no parallel write” (nopw) capabilities of these volumes. See also   
<https://help.jasmin.ac.uk/article/4700-understanding-new-jasmin-storage>


Thank you in advance for your cooperation.


JASMIN Team


