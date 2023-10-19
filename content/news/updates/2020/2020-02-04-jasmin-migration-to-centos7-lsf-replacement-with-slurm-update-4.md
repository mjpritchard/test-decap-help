---
title: JASMIN Migration to CentOS7 & LSF replacement with SLURM UPDATE 4
date: 2020-02-04 13:46:57+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-migration-to-centos7-lsf-replacement-with-slurm-update-4']
thumbnail: 
icon: fas circle-info
---

This is the latest update about migrating the JASMIN infrastructure from RedHat Enterprise Linux 6 (RHEL6) to CentOS7 and preparing for the replacement of the LSF batch scheduler with SLURM.


As stated in previous announcements, we are in the process of implementing a gradual transition of all “sci” servers and the LOTUS cluster to CentOS7. Additionally, we will replace the existing batch scheduler (Platform LSF) with SLURM. We have chosen SLURM because it is a cost-effective alternative which is widely used by other academic/scientific institutions (such as the UK Met Office).


These changes will affect nearly all JASMIN users so please take note!


The first scheduled changes are as follows:  
1. Two new “sci” servers, “sci[1,2].[jasmin.ac.uk/](http://jasmin.ac.uk/)”, will be created with the CentOS7 systems and the new software environments. These two VMs will be available and listed under the Message Of The Day on jasmin-login1, from mid-February. [Please note that the domain name of the servers has changed from “[.ceda.ac.uk/](https://www.ceda.ac.uk/)” to “[jasmin.ac.uk/](http://jasmin.ac.uk/)”].  
2. The “centos7" queue (currently used for testing) will be closed. A sub-cluster managed by SLURM will be deployed on Centos7 nodes. We will update JASMIN users with details and timeline soon.  
3. The transition period from LSF to SLURM is provisionally 6 months (February-31st July). During this period users are encouraged to migrate their workflows to the Centos7 queues which will be managed by SLURM.


Migration of the transfer, login and other general-purpose servers will be communicated in future announcements.


Previous announcements on this topic are detailed here: <http://www.jasmin.ac.uk/articles/vm-migration/>


Thank you for your attention and please look out for further updates as this work progresses.


CEDA and JASMIN Team


