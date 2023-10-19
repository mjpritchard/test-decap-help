---
title: JASMIN update on SLURM Scheduler upgrade
date: 2022-05-20 10:01:18+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-update-on-slurm-scheduler-upgrade']
thumbnail: 
icon: fas circle-info
---

Dear users,  
  



Further to our recent notice about forthcoming maintenance periods and upgrade to the SLURM scheduler, please note the following update:   
  



* The SLURM Scheduler upgrade is completed and LOTUS batch processing cluster is now available.


* The recommended method for launching an interactive job on LOTUS has changed. Resources have to be allocated exclusively to the interactive job step, and so creating other job steps, via mpirun, srun or other similar commands will not be able to access the resources and will hang. See details [here](https://help.jasmin.ac.uk/article/4890-how-to-submit-a-job-to-slurm)
* Generation of reports from SLURM accounting data is available for jobs submitted  in the new  SLURM version. Reports from the old SLURM will continue to be temporarily unavailable.
* The orchid partition remains offline as the upgrade has not been completed on the GPU nodes.


 


We had originally planned to update the version of LOTUS Slurm during August, but the announcement of a critical security update for Slurm meant that we were forced to update this week. As a result we have not been able to test the new SLURM version as thoroughly as we would have liked, so there may be issues related to the new version which we have not discovered.   
  



Many thanks for your patience  
  



JASMIN Team


