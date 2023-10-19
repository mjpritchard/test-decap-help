---
title: Reminder JASMIN Migration to CentOS7 & LSF replacement with SLURM UPDATE 13
date: 2020-11-16 09:56:27+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-migration-to-centos7-lsf-replacement-with-slurm-update-13']
thumbnail: 
icon: fas circle-info
---

Dear JASMIN users,


1. New MASS client server is available
2. Old *mass-cli1.ceda.ac.uk*  server will be retired on **Tuesday 17th November**
3. Old *jasmin-cylc.ceda.ac.uk* has been retired
4. JASPY default version was updated on **Tuesday 3rd November**
5. Reminder to use the new login, sci and xfer servers
6. SLURM update


##### Details of the update


1. The new CentOS7 MASS *mass-cli.jasmin.ac.uk* server is now available for use. 


2. Please migrate your workflows from the old *mass-cli1.ceda.ac.uk* server which will be turned off on **Tuesday 17th November.**


3. The old JASMIN cylc server *jasmin-cylc.ceda.ac.uk* was retired on **Tuesday 3rd November.** Please use the new JASMIN cylc server: *cylc.jasmin.ac.uk*


4. The default JASPY environment has been upgraded to: "jaspy/3.7/r20200606". This can be enabled using "*module load jaspy*" from **Tuesday 3rd November.** See: [here](https://help.jasmin.ac.uk/article/4729-jaspy-envs "here")


5. As previously announced, the old *login, xfer* and *sci* *servers* have now been retired. Please use the new servers with the new domain name *\*.jasmin.ac.uk* listed [here](https://help.jasmin.ac.uk/article/4859-centos7-sci-login-xfer-servers).  
  



6. SLURM update: As previously mentioned <https://www.ceda.ac.uk/blog/lotusslurm-issues-update/>,  we have now added more compute resources to LOTUS and redistributed them among specific SLURM scheduling queues. We continue to adjust the fair-share configuration of SLURM. It could take 2-3 weeks to have the desired effect on the overall jobs throughput. It is also anticipated that the SLURM scheduling queues will be restructured and a policy of resource usage and share between communities will be devised.   
  



**Support for parallel NetCDF libraries** (under /apps/jasmin/) is in progress. More information will be provided soon.


**Update on JASMIN software on CentOS7 hosted on "*/apps/contrib/*":** work is in progress to update and migrate software installed under: "*/apps/contrib/*" to a new partition “*/apps/jasmin/*”. More information will be provided soon. 


Thank you for your attention and please look out for further updates as this work progresses.  


CEDA and JASMIN Team


 



