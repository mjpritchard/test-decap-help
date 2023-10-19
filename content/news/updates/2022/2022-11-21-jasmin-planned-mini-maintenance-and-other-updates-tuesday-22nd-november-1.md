---
title: Reminder JASMIN planned mini maintenance and other updates - Tuesday 22nd November
date: 2022-11-21 10:02:29+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-planned-mini-maintenance-and-other-updates-tuesday-22nd-november-1']
thumbnail: 
icon: fas circle-info
---

Dear users,



Please note the upcoming “mini” maintenance day on **Tuesday 22nd November**. The following system work/enhancements are also planned for that date in order to minimise disruption:   
  



1. New scratch area and retiring /work/scratch-pw
2. SLURM configuration update
3. JASMIN accounts portal service upgrade
4. LOTUS at risk periods monthly schedule
5. Globus Connect Personal users: important update required
6. VIO7 at risk



Details:  
  
**1. New scratch area and retiring /work/scratch-pw**


A new 1 PB scratch volume will be made available at /work/scratch-pw3, which will replace the old volume /work/scratch-pw: 


* /work/scratch-pw will be made Read Only from **22nd November** with no further access from **15th December**
* Available scratch volumes from then on will be /work/scratch-pw2 /work/scratch-pw3, both 1 PB in size
* Any important data on /work/scratch-pw should be removed from that location before the **15th December 2022**


**2. Slurm configuration update**


As part of the continuous improvement to the Slurm scheduler, some of the Slurm configuration files will be migrated to a new location.


 


The LOTUS batch processing cluster will be unavailable for the duration of the work on the day, to avoid running jobs being adversely affected. **A reservation will start at 04:00 am on 22nd November till 02:00 pm** **on the day**, but any job submitted before 05:00 am with a running time that goes over the reservation period will not start until after the reservation has finished.


**3. JASMIN accounts portal upgrade**


A downtime is required to upgrade the JASMIN Accounts Portal service, the application where users can administer their own JASMIN accounts.


Whilst this downtime ought to be brief, access to <https://accounts.jasmin.ac.uk/> is considered at risk throughout the morning. The upgrade should provide performance improvements and reduce the need for downtimes for this service in the future.


**4. LOTUS at risk periods monthly schedule**


Going forward, we will be performing routine updates to the cluster LOTUS on a monthly basis. These are planned for **the second Tuesday of each month (6:00am-10:30am)**. Emergency/major updates may interrupt this schedule – notice will be provided - but this new, regular maintenance window should help users to plan their work around these incremental interventions while minimising disruption.


**5. Globus Connect Personal users: important update required**


Users who have installed instance(s) of Globus Connect Personal (software provided by Globus to run a local endpoint for data transfers) should already be aware via communications from Globus that an update is required in order to continue using the Globus service. Please see [this announcement](https://docs.globus.org/ca-update-2022/) and note the deadline of 12th December 2022.


**6. VIO7 at risk**


The switches for the cloud platform VIO7 will be upgraded. Please consider the services in the cloud at-risk on **22nd November**



Please note all the above updates and plan your work accordingly to minimise any inconvenience caused.



Thank you for your attention.



Best wishes,   
JASMIN Team


 


