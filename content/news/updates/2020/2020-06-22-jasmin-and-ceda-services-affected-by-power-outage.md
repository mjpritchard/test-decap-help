---
title: JASMIN and CEDA services affected by power outage - now resolved
date: 2020-06-22 17:14:59+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-and-ceda-services-affected-by-power-outage']
thumbnail: 
icon: fas circle-info
---

#### Update 1 - 22/06/2020 17:00


JASMIN and CEDA Archive services have been offline today due a power outage that affected the entire RAL site (including the JASMIN machine room) at approximately 13.30 on Monday 22 June 2020. The power is now back, but not all remaining actions can be carried out remotely. 


We are awaiting confirmation for when a member of the JASMIN team is allowed to enter the machine room. With the covid-19 restrictions in place, this will take longer than normal. 


At present, we do not know how long it will take for us to be able to gain access. Therefore, unfortunately, we cannot give you an estimate of when the services will be back up and running - it is looking unlikely that it will be today. 


#### Update 2 - 22/06/2020 18:00


Some limited services are back online but please consider all services AT RISK until further notice. 


#### Update 3 - 23/06/2020 10:30


Some services are back online but many are still affected by yesterday's power outage. Work is ongoing to restore these as quickly as possible. Please consider all services (CEDA Archive and JASMIN) at risk until further notice.   
  
Access to the JASMIN machine room is still necessary for some issues, as mentioned yesterday this will take longer than in normal circumstances (due to covid-19 restrictions). Unfortunately, we are unable to give an accurate timescale of when this can happen. 


#### Update 4 - 23/06/2020 17:00


* Some Much of JASMIN is now up, but for some significant components, work is still in progress.
* LOTUS nodes managed by LSF are up, SLURM-managed nodes to follow
* JASMIN Community Cloud is up (managed and external tenancies)
* Virtual Machines are up
	+ Some services on particular VMs may have dependencies which are still down
* Services in the Data Transfer Zone are still down
* Most storage volumes are accessible, however the following are still inaccessible pending completion of file system checks.



```
/work/scratch (old scratch volume, soon to be retired as per recent notices)
/datacentre/backupcache
/datacentre/processing3
/group_workspaces/jasmin2/clipc
/group_workspaces/jasmin2/cp4cds1/vol2
/group_workspaces/jasmin2/esacci_lst
/group_workspaces/jasmin2/globolakes
/group_workspaces/jasmin2/incompass
/group_workspaces/jasmin2/jules_OLD
/group_workspaces/jasmin2/leicester
/group_workspaces/jasmin2/nceo_aerosolfire
/group_workspaces/jasmin2/nceo_uor
/group_workspaces/jasmin2/precis

```



#### Update 5 - 24/06/2020 10:00


Much of JASMIN is now up and returning to normal service, with the exception of the components listed below:


- The "JASMIN GridFTP Server" Globus Endpoint (data-xfer1.ceda.ac.uk) is still down, but all other services in the Data Transfer Zone are working normally.


- Most storage volumes are accessible, however the following are still inaccessible pending completion of file system checks:


/work/scratch (old scratch volume, soon to be retired as per recent notices)


/datacentre/processing3


/group\_workspaces/jasmin2/nceo\_aerosolfire


 


Please report any further problems you encounter to support@jasmin.ac.uk but please continue to bear with us as resolving problems may still take longer than normal.  
  



#### Update 6 - 26/06/2020 15:00


  
We believe all JASMIN and CEDA Archive services are now working after Monday’s power outage. If you believe anything isn’t working correctly, please let us know by contacting the [appropriate helpdesk](https://www.ceda.ac.uk/contact/).  
  
A few of you have asked why JASMIN doesn’t have some form of back up, so we thought it might be useful to share the reason with you all. JASMIN has a power demand of around 200kW from ~50 full racks of equipment, network and tape robot infrastructure. It shares its machine room environment and some of these systems with facilities of similar scale for other communities and hence a power backup of suitable capacity and complexity would be prohibitively expensive for the science (rather than enterprise) budgets we’re working within. Many subsystems within JASMIN already run on UPS systems to provide short-term supply enabling clean shutdown, but continued operation without mains power is not something which is currently feasible.


  
  



#### Future updates:


We will update the status of the situation as it progresses via [Twitter](https://twitter.com/cedanews), our [news channel](https://www.ceda.ac.uk/blog/) and the JASMIN mailing lists. Please check here for further updates. 


We will keep monitoring the situation and will send another update soon.


JASMIN Team


