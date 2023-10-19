---
title: System maintenance Tues 15 Sept 2020
date: 2020-09-14 15:51:50+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/system-maintenance-tues-15-sept-2020']
thumbnail: 
icon: fas circle-info
---

Scheduled maintenance is planned for Tuesday 15th September, which may cause some disruption to JASMIN and CEDA services.


On a regular (roughly quarterly) basis, important updates are applied to systems within the JASMIN infrastructure (which also hosts the CEDA Archive and associated services) in order to keep them up to date and secure. Some servers may need to be rebooted in order for these changes to take effect, so there may be an interruption to some JASMIN and CEDA services on this date. The maintenance work will also include a network change which should help prevent recent problems experienced with the virtualization cluster.


The LOTUS batch processing cluster will be unavailable for the duration of the JASMIN maintenance work, to avoid running jobs being adversely affected. The batch reservation will start at **05:00 AM on Tuesday 15th September**, but any job submitted before that with a running time that goes over the reservation period will not start until after the reservation has finished.


Note: The SLURM parallel queue ‘par-multi’ was placed in down state at **12:30PM today (14th September)** ahead of tomorrow's maintenance day for further queue configuration work. The ‘par-multi’ will not be available until after the JASMIN maintenance day.



JASMIN Team


