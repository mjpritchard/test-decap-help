---
title: JASMIN update on SLURM Scheduler upgrade - starts Friday 13th May 2022
date: 2022-05-13 08:30:29+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-update-on-slurm-scheduler-upgrade-starts-friday-13th-may-2022']
thumbnail: 
icon: fas circle-info
---

Dear users,  
  



Further to our recent notice about forthcoming maintenance periods and upgrade to the SLURM scheduler, please note the following update:   
  



SLURM Scheduler upgrade - now starting Friday 13th May 2022  
  



The LOTUS batch processing cluster will need to be taken down to perform important updates on the SLURM scheduling software during the week commencing 16th May 2022. The core of the upgrade work should take no longer than 2 days, but preparations to enable the work to proceed safely will mean that LOTUS is not available to users for a longer period around those dates. 


* A reservation for the entire period is already in place and will be lifted once the work has been completed (later in the week 16-20 May).
* All SLURM queues/partitions will be closed on Friday 13th May at 22:00 hrs: this means no further jobs can be submitted after that time. The following error message would be encountered “Batch job submission failed: Required partition not available (inactive or drain)”
* Due to the nature and extent of the work, jobs still pending on Tuesday 17th May 2022 08:00 will unfortunately be lost.  We advise users to keep a record of their pending jobs and resubmit them to SLURM once completion of the work has been announced, expected later in the week of 16-20 May.
* Generation of reports from SLURM accounting data will also be temporarily unavailable throughout this period.


We apologise for the inconvenience this may cause and for the short notice: please note that jobs with long expected run times will already be affected by the reservation now in place.  
  



JASMIN Team


