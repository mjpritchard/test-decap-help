---
title: JASMIN storage issues and update on network connectivity
date: 2021-04-22 15:55:40+00:00
tags: ['news', 'jasmin ceda']
aliases: ['/blog/jasmin-storage-issues-and-update-on-network-connectivity']
thumbnail: 
icon: fas circle-info
---

We are aware of current issues with one of the JASMIN storage systems. While investigations are still ongoing, the current status is as follows.


* Storage affected:
+ some Group Workspaces (those with /gws/nopw/j04 paths)
+ some CEDA Archive datasets (multiple datasets, unfortunately there is no easy way for us to inform you which datasets are affected)

* Issue 1:
+ This appears as intermittent I/O Errors when trying to access a file or directory. It is caused by a problem with the software used to access the storage from the machine where you may be working. A fix for this issue will be released in the next version of the software when available from the vendor and applied across the platform at the earliest opportunity.
+ Short-term solution: For now, the recommended workaround for users is to move to a different machine if possible.

* Issue 2:
+ This appears as file systems appearing to hang/freeze and becoming unavailable. The vendor is currently investigating and actively trying to fix this issue, but has not yet identified a solution.
+ Short-term solution: A workaround for now would be to try accessing the same filesystem from a different machine (where it should still be mounted) or try again later from the same machine.


  
Please also be aware that as of 14:30 today, the RAL site is still experiencing some network connectivity issues following yesterday’s RAL firewall changes. We await further information but we are told that if the situation has not stabilised by the end of today it is possible that yesterday’s changes may be rolled back. Therefore network connectivity to JASMIN and CEDA services to/from the outside world should be regarded as “at risk” until further notice.  
  
We apologise for any inconvenience caused by these issues.  
JASMIN Team


