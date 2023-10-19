---
title: JASMIN login services are available - issue resolved
date: 2023-02-28 11:59:35+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-login-services-are-available-issue-resolved']
thumbnail: 
icon: fas circle-info
---

Dear JASMIN user,



We believe that the recent issue that affected the PURE storage system that hosts the home users directories and some small-files group workspaces is now resolved and JASMIN login services are operational.



The PURE storage system that hosts the home users directories exhibited issues related to parallel-write/read locks with some impacts to system performance as a whole. The relevant processes were identified and modified to avoid this happening.



Users are reminded that processes which require parallel write access to a file, particularly at scale (for example, if many LOTUS jobs need to update the same file), should make use of PFS storage such as the */work/scratch-pw[2,3]* volumes, and should be tested before large-scale execution. 


Please see <https://help.jasmin.ac.uk/article/176-storage> for information about types and location of storage.



Thank you for your patience and cooperation 



JASMIN team 


 


