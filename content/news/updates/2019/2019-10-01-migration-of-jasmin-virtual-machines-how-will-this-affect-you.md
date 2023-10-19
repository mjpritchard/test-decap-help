---
title: Migration of JASMIN virtual machines - how will this affect you?
date: 2019-10-01 12:05:49+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/migration-of-jasmin-virtual-machines-how-will-this-affect-you']
thumbnail: 
icon: fas circle-info
---
**RHEL6 virtual machines to be migrated to CentOS7**  
Currently, many CEDA and JASMIN services are hosted using virtual machines (VMs) which run on RedHat Enterprise Linux 6 (RHEL6). These will soon need to be migrated to VMs based on the CentOS7 operating system. This is because:


* The UKRI/STFC site license agreement for RedHat Enterprise Linux is coming to an end.


	+ The decision has been taken to move to the open-source equivalent, CentOS.
* RHEL6 and its open-source equivalent, CentOS6 are approaching end-of-life, after which it will not be possible to obtain important package updates for these systems.
	+ Security requirements can only be met by using operating systems which are currently supported and for which package updates are available on a timely basis.


The CEDA JASMIN team is currently planning how this can take place with the minimum of disruption but in a manner which prioritises security.  
  
We have created [this web page](http://www.jasmin.ac.uk/articles/vm-migration/) which will provide updates on this process.  
  
**JASPY: a new system for deploying “JASMIN Analysis Platform” software**  
In parallel with the above activity to migrate individual VMs, work is underway to provide a new delivery method for the “JASMIN Analysis Platform” software, which is the stack of software currently maintained and deployed across the [scientific analysis servers](https://help.jasmin.ac.uk/article/121-sci-servers), the [LOTUS batch processing cluster](https://help.jasmin.ac.uk/article/110-lotus-overview) and a number of bespoke VMs.  
  
The new system, known as “JASPY”, will be based around the “conda” system for creating the core Python environments in Python 2.7 and Python 3.7. JASPY is documented [here](https://help.jasmin.ac.uk/article/4729-jaspy-envs).  
  
Further information about this activity and about plans for deployment of this software on scientific analysis servers and LOTUS nodes, will be added to the web page in due course.  
  
**How will this affect me?**  
Some CEDA Archive and JASMIN services will be migrated to new servers over the next few months: there may be some disruption to individual services as they are redeployed, but announcements regarding particular services will be made in due course.  
  
Regular users of the scientific analysis servers and/or LOTUS are recommended to read information about the JASPY system and about the move to CentOS7 on these systems, as it becomes available.  
  
More detailed timescales and changes to individual services will be announced in due course.  
  
CEDA JASMIN Team

