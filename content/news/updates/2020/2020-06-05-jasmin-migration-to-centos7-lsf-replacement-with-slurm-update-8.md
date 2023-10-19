---
title: JASMIN Migration to CentOS7 & LSF replacement with SLURM UPDATE 8
date: 2020-06-05 10:56:13+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-migration-to-centos7-lsf-replacement-with-slurm-update-8']
thumbnail: 
icon: fas circle-info
---

Dear JASMIN users,  
  
This message includes information about the following:  
  
1. Update on SLURM & CentOS7 LOTUS cluster  
2. New MPI implementation on LOTUS   
3. SLURM/LOTUS webinar  
4. LSF-managed LOTUS resources to be reduced from mid-June.  
  
**Important reminder about the timescale:** the current batch system will be **unavailable after the end of June 2020**. After this, users will be expected to use SLURM.  
  
Details of the update  
  
1. A sub-cluster of LOTUS with the CentOS7 systems, and managed by the new batch scheduler SLURM, is now available for testing using the serial and the parallel SLURM queues (partitions): ‘short-serial’, ‘test’. ‘par-single’ and ‘par-multi’. All LOTUS users should familiarise with SLURM ahead of the changeover. See:   
<https://help.jasmin.ac.uk/category/4889-slurm>  
  
2. The OpenMPI library is the only supported MPI library on the CentOS7 cluster managed by SLURM. OpenMPI v3.1.1 and v4.0.0 are provided which are fully MPI3-compliant. See:  
<https://help.jasmin.ac.uk/article/4896-how-to-submit-an-mpi-parallel-job-to-slurm>


  
3. A webinar on transitioning from LSF to SLURM is scheduled on Thursday 18th June. Further details will be provided in due course.  
  
4. LSF-managed LOTUS resources will be reduced from mid-June. All LOTUS hosts will be moved to CentOS7 and managed by SLURM by the end of June.   
  
**Plans for updates to mass-cli1 and jasmin-cylc servers:** We are currently working on replacements for the "mass-cli1" and "jasmin-cylc" servers. More information about the new configurations will be provided in future communications.   
  
Previous announcements on this topic are detailed here: [http://www.jasmin.ac.uk/articles/vm-migration/](http://www.jasmin.ac.uk/articles/vm-migration/ )   
  
Thank you for your attention and please look out for further updates as this work progresses.  
  
CEDA and JASMIN Team


