---
title: JASMIN upgrade reminders and further information 
date: 2018-03-07 16:54:48+00:00
tags: ['news']
aliases: ['/blog/jasmin-upgrade-reminders-and-further-information']
thumbnail: 
icon: fas circle-info
---
1. JASMIN Unavailability Wednesday 14th March (see previous email)  
2. Changes to Group Workspace Storage (see previous email)  
3. Changes to /work/scratch storage.  
4. Draining of LOTUS jobs starts TODAY 7th March.  
5. General "at risk" during phase4 installation work.


For Items 1 & 2, please refer to our earlier announcement of 23/02/2018 or visit http://www.jasmin.ac.uk/phase4 for details.


REMINDER:  
MOST OF JASMIN WILL BE UNAVAILABLE 07:00 - 19:00 ON WEDNESDAY 14TH MARCH 2018 - Although this unavailability should not affect virtual machines running in the JASMIN Unmanaged Cloud, any data services which they rely on in the main JASMIN infrastructure should be regarded as unavailable or at least at high risk of interruption on that day.


In addition, please be aware of the following:  
3. On 14th March, /work/scratch (used as intermediate storage by LOTUS jobs, not for general interactive use) will be set up on new storage. The following steps will take place:  
a) Existing "/work/scratch" will be renamed "/work-scratch-OLD" and made READ-ONLY.  
b) A new "/work/scratch" area will be created (same size) on newer storage. However, you should configure your software to use this ONLY if you think you need shared file writes with MPI-IO.  
c) A second, larger area, "/work/scratch-nompiio" will be created (estimated size 250TB) on new flash-based storage which should have significant performance benefits particularly for operations involving lots of small files.


4. In advance of (3), a reservation is already in place to drain LOTUS of jobs so that this work can take place as scheduled. From today (7th March), 7-day jobs will not be scheduled. From tomorrow, 6-day jobs will not, and so on. Normal LOTUS service should resume once the work has completed on 14th March.


5. During the entire period from now until mid-April, there is the possibility of further unplanned interruptions to aspects of the infrastructure while installation work is carried out. No further planned downtimes are currently scheduled, but the nature of the work involved carries some risk that unscheduled incidents may occur.


We thank you in advance for your cooperation with these changes while the next generation of JASMIN technology is brought into operation and look forward to telling you more about them as the work progresses.


JASMIN Team

