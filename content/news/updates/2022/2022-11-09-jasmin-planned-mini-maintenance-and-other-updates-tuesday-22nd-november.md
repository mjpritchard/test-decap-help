---
title: JASMIN planned mini maintenance and other updates - Tuesday 22nd November
date: 2022-11-09 09:59:16+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-planned-mini-maintenance-and-other-updates-tuesday-22nd-november']
thumbnail: 
icon: fas circle-info
---

Dear users,



Please note the upcoming “mini” maintenance day on **Tuesday 22nd November**. The following system work/enhancements are also planned for that date in order to minimise disruption: 


1. PFS storage update
2. New scratch area and retiring /work/scratch/pw
3. SLURM configuration update
4. JASMIN accounts portal service upgrade
5. LOTUS at risk periods monthly schedule
6. Globus Connect Personal users: important update required



Details:



1. **PFS storage update**  
Postponed from our recent October maintenance day, this work will now take place on **Tuesday 22nd  November**. Servers and clients of the parallel file system (PFS) storage will be updated. Among other updates, this should address current issues with the PFS disk space usage reporting utility pan\_df.



2. **New scratch area and retiring /work/scratch/pw**


A new 1 PB scratch volume will be made available at /work/scratch-pw3, which will replace the old volume /work/scratch-pw: 



* /work/scratch/pw will be made Read Only from **22nd November** with no further access from **15th December**
* Available scratch volumes from then on will be /work/scratch/pw2 /work/scratch/pw3, both 1 PB in size
* Any important data on /work/scratch/pw should be removed from that location **before the 15th December 2022**



3. **Slurm configuration update**


As part of the continuous improvement to the Slurm scheduler, new features will be enabled on the scheduler to manage the load and control resources allocation for accessing the queues. 



The LOTUS batch processing cluster will be unavailable for the duration of the work on the day, to avoid running jobs being adversely affected. **A reservation will start at 05:00 am on 22nd November till 02:00 pm****on the day**, but any job submitted before 05:00 am with a running time that goes over the reservation period will not start until after the reservation has finished.



**IMPORTANT**: No jobs will be accepted by SLURM from  **05:00 am on 22nd November****until the reservation is lifted**. Any attempt to submit a job to SLURM will be rejected with the following message: 


sbatch: error: Batch job submission failed: Required partition not available (inactive or drain)



4. **JASMIN accounts portal upgrade**


A downtime is required to upgrade the JASMIN Accounts Portal service, the application where users can administer their own JASMIN accounts.


Whilst this downtime ought to be brief, access to <https://accounts.jasmin.ac.uk/> is considered at risk throughout the morning. The upgrade should provide performance improvements and reduce the need for downtimes for this service in future.



5. **LOTUS at risk periods monthly schedule**


Going forward, we will be performing routine updates to the cluster LOTUS on a monthly basis. These are planned for **the second Tuesday of each month (8:00am-10:30am)**. Emergency/major updates may interrupt this schedule – notice will be provided - but this new, regular maintenance window should help users to plan their work around these incremental interventions while minimising disruption.



6. **Globus Connect Personal users: important update required**


Users who have installed instance(s) of Globus Connect Personal (software provided by Globus to run a local endpoint for data transfers) should already be aware via communications from Globus that an update is required in order to continue using the Globus service. Please see [this announcement](https://docs.globus.org/ca-update-2022/) and note the deadline of **12th December 2022**.



Please note all the above updates and plan your work accordingly to minimise any inconvenience caused.



Thank you for your attention.



Best wishes,

JASMIN team
