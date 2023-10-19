---
title: Reminder JASMIN mini-patch day Tomorrow - Tuesday 21st March 2023
date: 2023-03-20 12:17:22+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-mini-patch-day-tuesday-21st-march-2023']
thumbnail: 
icon: fas circle-info
---

Dear JASMIN user,



Please note the upcoming “mini” maintenance day on **Tuesday 21st March**. The following system work/enhancements are also planned for that date in order to minimise disruption: 



1. PFS storage update
2. Changes to */tmp* quota (postponed previously)
3. New SSD scratch area replacing */work/scratch-nopw*
4. Shutdown of sci3 pending replacement
5. Changes nfsaf01 migration (home dirs & gws/smf : no path change), move ncas-radar PURE volume
6. Changes to network subnets


 


Details:



1. Parallel File System (PFS) Storage update


A final part of the recent update to parallel file system (PFS) storage will be completed. This affects some CEDA Archive services, group workspaces with */gws/pw/j07* paths and XFC (transfer cache) volumes.



2. Changes to */tmp* quota


A per-user limit of 500MB will be introduced on */tmp* storage volumes on sci servers *sci[1,2,4,5]*.  Please ensure that your processes avoid using */tmp* on individual machines, instead use scratch storage. This work was postponed from a previous maintenance day.



3. New SSD scratch area replacing */work/scratch-nopw*


A new 90TB  scratch volume will be made available at */work/scratch-nopw2*, which will replace the old volume */work/scratch-nopw*: 



* */work/scratch-nopw* will be made Read Only from **21st  March** with no further access after **1st May 2023**
* Any important data on */work/scratch-nopw* should be removed from that location before **1st May 2023**



4. Shutdown of sci3 pending replacement


We are aware of memory errors reported by the kernel/system on the sci machine *sci3.jasmin.ac.uk*. The warning messages from "*syslogd@host595*" should not affect the processes running on sci3 as the error is correctable. However, a decision has been made to shut sci3 down until a replacement becomes available.


Please consider using the other two high-memory sci machines sci6 and sci8 to avoid the annoying console messages for now



5. Changes to storage used for HOME and SMF areas.
* User home directories */home/users* and the small-file group workspaces under */gws/smf/* will be migrated to new storage. Once migrated, they will be available again with no path change, so the change should be transparent to users
* Likewise, the ncas\_radar SSD volume will be migrated but with no path change.



6. Changes to network subnets


The network subnets changes will allow migration from legacy networks. It might cause VMs to be briefly inaccessible (it will not affect JASMIN cloud)



The LOTUS batch processing cluster will be unavailable for the duration of the work on the day, to avoid running jobs being adversely affected. **A reservation will start at 04:00 am on 21st March till 23:59 pm on the day**, but any job submitted before 04:00 am with a running time that goes over the reservation period will not start until after the reservation has finished.



Please note all the above updates and plan your work accordingly to minimise any inconvenience caused.



Thank you for your attention.



Best wishes,   
JASMIN Team


 


