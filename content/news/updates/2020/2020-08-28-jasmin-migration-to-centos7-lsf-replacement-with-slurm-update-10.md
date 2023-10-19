---
title: Reminder JASMIN Migration to CentOS7 & LSF replacement with SLURM UPDATE 10
date: 2020-08-28 09:22:34+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-migration-to-centos7-lsf-replacement-with-slurm-update-10']
thumbnail: 
icon: fas circle-info
---

Dear JASMIN users,  
  
This message includes information about the following:  
  
1. Update on SLURM and the CentOS7 LOTUS cluster  
2. Timeline to retire old RHEL6 login, sci and data transfer servers  
3. New high-memory CentOS7 sci machines  
  
Details of the update  
  
1. LOTUS resources under LSF have been converted over to SLURM. All LOTUS users are expected to use SLURM. For details, please see our webinar and presentation on transitioning from LSF to SLURM: [https://www.ceda.ac.uk/events/transitioning-to-slurm-webinar](https://www.ceda.ac.uk/events/transitioning-to-slurm-webinar/)   
  
More information about SLURM is available on our help pages:<https://help.jasmin.ac.uk/category/4889-slurm>  
  
2. The following RHEL6 "login", "sci" and data transfer ("xfer") servers **will be retired on Tuesday 15th September**:   
  
login servers:  
*jasmin-login1.ceda.ac.uk*  
*jasmin-login2.ceda.ac.uk*  
*jasmin-login3.ceda.ac.uk*  
*jasmin-login4.ceda.ac.uk*  
*cems-login1.cems.rl.ac.uk*  
*comm-login1.cems.rl.ac.uk*


sci servers:   
*jasmin-sci1.ceda.ac.uk*  
*jasmin-sci2.ceda.ac.uk*  
*jasmin-sci4.ceda.ac.uk*  
*jasmin-sci5.ceda.ac.uk*  
*cems-sci1.cems.rl.ac.uk*


xfer servers:  
*jasmin-xfer1.ceda.ac.uk*  
*cems-xfer1.cems.rl.ac.uk*


All JASMIN users are expected to use the new CentOS7 login servers (*login[1,2,4].jasmin.ac.uk*), scientific analysis servers (*sci[1,2,4,5].jasmin.ac.uk*) and the data transfer servers (*xfer[1,2].jasmin.ac.uk*). Further details can be found here: <https://help.jasmin.ac.uk/article/4859-centos7-sci-login-xfer-servers>  
3. The new high-memory CentOS7 scientific analysis server with SLURM enabled will be available for users to test out from next week.  
  
**Plans for updates to mass-cli1**: We are currently working on replacements for the "mass-cli1". More information about the new configurations will be provided in future communications.   
  
**Update on JASMIN software** on CentOS7 hosted on "/apps/contrib/": work is in progress to update and migrate software installed under: "/apps/contrib/". More information will be provided soon.  
  
Previous announcements on this topic are detailed here: <http://www.jasmin.ac.uk/articles/vm-migration/>  
  
Thank you for your attention and please look out for further updates as this work progresses.   
  
Please note our services will be unsupported on Monday 31st August and Tuesday 1st September due to the UK bank holiday. Any issues that may arise over the weekend will not be looked at by the team until Wednesday 2nd September.   
  
CEDA and JASMIN Team


