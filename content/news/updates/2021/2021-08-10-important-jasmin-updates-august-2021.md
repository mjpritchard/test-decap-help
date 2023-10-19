---
title: Important JASMIN updates August 2021
date: 2021-08-10 08:02:20+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/important-jasmin-updates-august-2021']
thumbnail: 
icon: fas circle-info
---

Dear JASMIN users,  
  
This message includes information about important updates on JASMIN:  
  
1. Kernel patching required on all JASMIN login, sci and data transfer servers   
2. Kernel patching required across all LOTUS compute nodes  
3. Maximum job array size and default memory allocation to be changed  
4. Short-serial-4hr queue configuration has changed  
   
Details of the update  
  
1. The Kernel patching will be carried out as a rolling update from today on all login, sci and data transfer servers. The down time will be less than 5 min and it will be every 30 min that a JASMIN server is rebooted. Please save your work and logout when the “rebooting” message is broadcasted on your terminal session.  
  
2. Kernel patching required across all LOTUS computed nodes has started as a rolling update. A number of nodes will be drained from the SLURM queues for this update. The wait time per job might slightly be affected. This rolling update will continue over the next week from Today.  
  
3. The maximum array size per job array will be changed to 10000 and the default memory size allocation will be decreased from 8 GB to 4 GB


4. The provisional ‘short-serial-4hr’ SLURM partition/queue is now associated with a new account ‘short-4hr’. Anyone wanting to use the 'short-serial-4hr' queue now needs to specify the SLURM '--account=short4hr'. In addition, the short-serial-4hr will only have AMD node type.


Thank you for your attention and please look out for further updates as this work progresses.   
JASMIN Team


