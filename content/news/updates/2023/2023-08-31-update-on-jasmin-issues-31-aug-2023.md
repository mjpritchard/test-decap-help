---
title: Update on JASMIN issues 31 Aug 2023
date: 2023-08-31 14:54:40+00:00
tags: ['news']
aliases: ['/blog/update-on-jasmin-issues-31-aug-2023']
thumbnail: 
icon: fas circle-info
---

Dear users,



We thank you for your patience while the system team has been working to resolve the network and storage issues of the past few days. The current situation is as follows:



* Migration of data from /gws/smf/\* (small-files group workspaces) and /apps/jasmin (used for software including the “modules” system) has now been completed and once other systems return to normal, no changes should be apparent to users.
* At the time of writing, LOTUS nodes are currently in a state of either
+ Fixed but currently idle, pending (imminent) re-opening of queues
+ Stuck with failing or failed jobs, awaiting reboot
+ Shortly, queues will be re-enabled so will start processing jobs again, but initially at a slower rate than normal until nodes in state (a) have been rebooted. [STOP PRESS: now reopened]

* Other systems needing to mount group workspace storage (including /gws/smf) will need rebooting in order to work correctly again.
+ General purpose sci VMs may need to be rebooted in due course
+ Managers of tenancy sci machines (\*-sci-M tenancies in JASMIN cloud) are requested to reboot their own sci machines themselves via the cloud portal
+ Other services such as cron, cylc etc will be rebooted in due course.

* The network issue is believed to be a recurrence of a hardware-related issue. It has been temporarily resolved but the possibility of further breaks remains. A further intervention is required (ideally to be scheduled in due course) but the risk of further interruptions does remain until this has been done.



In summary: users can start using services again, but systems are still “at risk” and LOTUS throughput may initially be slower than normal.



With apologies for any inconvenience caused,



JASMIN Team


 


