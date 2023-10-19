---
title: Reminder - JASMIN‌ ‌Migration‌ ‌to‌ ‌CentOS7‌ ‌&‌ ‌LSF‌ ‌replacement‌ ‌with‌ ‌SLURM‌ ‌UPDATE‌ ‌12‌
date: 2020-10-26 11:36:33+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-migration-to-centos7-lsf-replacement-with-slurm-update-12']
thumbnail: 
icon: fas circle-info
---

Dear JASMIN users,  
  
1. New CentOS7 MASS client server  
2. Old *jasmin-cylc.ceda.ac.uk* to be retired on **Tuesday 3rd November.**  
3. JASPY default version will be updated on **Tuesday 3rd November.**  
4. Reminder to use the new login, sci and xfer servers  
5. Closing down LSF and removing access to LOTUS head node  
6. Support for parallel NetCDF libraries (under */apps/jasmin/*)  
7. ESMValTool installed on JASMIN  
  
Details of the update  
  
1. The new CentOS7 MASS *mass-cli.jasmin.ac.uk* server is now available for use. Please migrate your workflows from the old *mass-cli1.ceda.ac.uk* server which will be turned off on **Tuesday 17th November** .   
  
2. The old JASMIN cylc server *jasmin-cylc.ceda.ac.uk* will be retired on **Tuesday 3rd November**. Please use the new JASMIN cylc server *cylc.jasmin.ac.uk*


3. The JASPY module environment available via ‘*module add jaspy*’ will by default enable the most recent release of JASPY such as "jaspy/3.7/r20200606" from **Tuesday 3rd November**. See: [here](https://help.jasmin.ac.uk/article/4729-jaspy-envs)


4. As previously announced, old login, xfer and sci servers have now been retired. Please use the new servers with the new domain name *\*.jasmin.ac.uk* listed [here](https://help.jasmin.ac.uk/article/4859-centos7-sci-login-xfer-servers).


5. The old batch scheduler LSF will be closed and access to the LOTUS head node *lotus.jc.rl.ac.uk* will be disabled on **Wednesday 28th October**. If you need to retrieve any job accounting information from past jobs (up to the last 3 months) on LSF so please do as soon as possible. We will proceed with the decommissioning plan for LSF very soon.


6. Support for parallel NetCDF libraries (under */apps/jasmin/*) is in progress. More information will be provided soon.


7. ESMValTool installed on JASMIN: the Earth System Model Evaluation Tool (ESMValTool) has been installed on JASMIN as a *community package*. See more info [here](https://help.jasmin.ac.uk/article/4955-community-software-esmvaltool).  
  
**SLURM performance:** An update about current SLURM performance issues will be provided in a separate communication before the end of this week.   
  
**Update on JASMIN software on CentOS7 hosted on "*/apps/contrib/*"**: work is in progress to update and migrate software installed under: "*/apps/contrib/*" to a new partition “*/apps/jasmin/*”. More information will be provided soon.   
  
Thank you for your attention and please look out for further updates as this work progresses.   
  
CEDA and JASMIN Team


