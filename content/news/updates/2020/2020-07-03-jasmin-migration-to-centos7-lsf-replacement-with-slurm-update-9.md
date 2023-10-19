---
title: JASMIN Migration to CentOS7 & LSF replacement with SLURM UPDATE 9
date: 2020-07-03 10:59:06+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-migration-to-centos7-lsf-replacement-with-slurm-update-9']
thumbnail: 
icon: fas circle-info
---

This message includes information about the following:


1. Update on SLURM & CentOS7 LOTUS cluster
2. sci[1,2].jasmin.ac.uk with SLURM enabled
3. New CentOS7 JASMIN cylc server
4. New CentOS7 cron server


##### Details of the update


1.  More LOTUS hosts have been migrated to CentOS7 and added to the pool of hosts managed by the new batch scheduler SLURM.  All LOTUS users are expected to use SLURM. The recording and PPT presentation of the first webinar on transitioning from LSF to SLURM are now available at <https://www.ceda.ac.uk/events/transitioning-to-slurm-webinar>  


See SLURM documentation: <https://help.jasmin.ac.uk/category/4889-slurm>  


2. The CentOS7 scientific analysis servers (sci1.jasmin.ac.uk and sci2.jasmin.ac.uk) have now been reconfigured to enable SLURM job submission.


3. The new CentOS7 cylc server cylc.jasmin.ac.uk with SLURM enabled is available for users to test out. Please note that the environment variable for the new cylc server has to be set to /apps/jasmin/metomi/bin



```
if [[ $(hostname) =~ ^cylc ]] ; then
```


```
   export PATH=/apps/jasmin/metomi/bin:$PATH
```


```
fi
```

4. The new Centos7 JASMIN cron server cron.jasmin.ac.uk with SLURM enabled is available for users to use.


Plans for updates to mass-cli1: We are currently working on replacements for the "mass-cli1". More information about the new configurations will be provided in future communications. 


Update on JASMIN software on CentOS7 (/apps/contrib...) work is in progress


Previous announcements on this topic are detailed here: <http://www.jasmin.ac.uk/articles/vm-migration/> 


Thank you for your attention and please look out for further updates as this work progresses.



CEDA and JASMIN Team


