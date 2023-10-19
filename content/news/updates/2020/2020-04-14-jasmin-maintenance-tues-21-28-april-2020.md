---
title: JASMIN Maintenance Tues 21 & 28 April 2020
date: 2020-04-14 09:29:51+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-maintenance-tues-21-28-april-2020']
thumbnail: 
icon: fas circle-info
---

Scheduled maintenance is planned for Tuesday 21st AND 28th April 2020, some of which will result in disruption to JASMIN systems, services and data in addition to the CEDA Archive.  
   
The following work is currently scheduled for these dates:  
   
21st April : disruption due to network maintenance and quarterly patch updates  
1. There will be a small network change which will interrupt storage visibility for ALL virtual machines (and any JASMIN or CEDA services running on them) for at least part of the day. This is part of a long programme of work to improve storage access and reliability during 2020.  
2. Once that change is stable, the usual quarterly patch updates will proceed, including rebooting of servers where necessary for the changes to take effect.


28th April : “At risk”  
1. On this date the Quobyte storage servers will have their network card firmware and driver software updated. This can be done one server at a time and so should be transparent to users. However there is some risk of disruption so please be aware.  
   
The LOTUS batch processing cluster will be unavailable for the duration of the work on 21st April to avoid running jobs being adversely affected. The reservation will start at 06:00 on 21st April, but any job submitted before that with a running time that goes over the reservation period will not start until after the reservation has finished.


With apologies for any inconvenience caused,


JASMIN Team


