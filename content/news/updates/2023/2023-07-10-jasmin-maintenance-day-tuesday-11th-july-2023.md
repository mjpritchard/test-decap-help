---
title: Final Reminder - JASMIN maintenance day Tomorrow, Tuesday 11th July 2023
date: 2023-07-10 10:19:42+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-maintenance-day-tuesday-11th-july-2023']
thumbnail: 
icon: fas circle-info
---

Dear JASMIN user,

This is the final reminder to please note the upcoming maintenance day Tomorrow, Tuesday 11th July. The following system work/enhancements are also planned for that date in order to minimise disruption:

1. Disable write access to the old scratch area `/work/scratch-nopw`
2. Increase the size of current SSD scratch area `/work/scratch-nopw2`
3. Slurm configuration update
4. Changes to cloud firewall
5. Changes to network routing

Details:

1. Disable write access to the old scratch area `/work/scratch-nopw`

    The old volume `/work/scratch-nopw` has previously been announced as out of service but the following steps will now implement this:

    * `/work/scratch-nopw` will be made read-only from 11th July with no access after 18th July 2023
    * Any important data on `/work/scratch-nopw` should be copied from that location before 18th July 2023

2. Increase the size of the current SSD scratch area `/work/scratch-nopw2`

    The size of `/work/scratch-nopw2` will be expanded from 90TB to 200TB. The per-user quota limit of 5TB will be increased.  

3. Slurm configuration update

    As part of the continuous improvement to the Slurm scheduler, new features will be enabled on the scheduler to manage the load and control resources allocation for accessing the queues.

4. Changes to network routing

    Some network changes are planned to enable new storage hardware to be accessible throughout JASMIN.

5. Changes to the cloud firewall

    The firewall serving the JASMIN community cloud is to be replaced.

The LOTUS batch processing cluster will be unavailable for the duration of the work on the day, to avoid running jobs being adversely affected. A reservation will start at 05:00 am on  11th July till 23:59 pm on the day, but any job submitted before 04:00 am with a running time that goes over the reservation period will not start until after the reservation has finished.

Please note all the above updates and plan your work accordingly to minimise any inconvenience caused.

Thank you for your attention.

Best wishes,

JASMIN Team
