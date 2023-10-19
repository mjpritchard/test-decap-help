---
title: LOTUS/SLURM issues update
date: 2020-10-06 08:53:22+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/lotusslurm-issues-update']
thumbnail: 
icon: fas circle-info
---

Dear all,


As you know we have recently seen some problems with the SLURM scheduler for the LOTUS batch processing cluster, with jobs remaining in the pending state for much longer than normal. This issue has been and remains a top priority for the JASMIN team to resolve. Here's the current state of affairs:  
**• Today (Monday 5 Oct)**  
o Fair-share configuration has been adjusted to attempt to lower the priority of very large/long-running jobs (which were causing sections of the cluster to become blocked)  
o An even mix of user ids is now being seen with running and pending jobs, implying that jobs are now starting to flow more normally, without being dominated by any one user.  
o A fix to a storage client has been rolled out to some parts of JASMIN which fixes a write issue for some users (NB not necessarily related to scheduling issues)  
  
• **Thurs/Fri last week**  
o Clean-up of existing thousands of hung jobs  
o 2 users in particular had issues with parallel write to storage, which were inadvertently causing wider disruption: users contacted/advised accordingly  
  
• **Following days this week (planned)**  
o Adjusting configuration of some queues to improve overall throughput (relevant user/groups will be contacted)  
o Continuing rollout of storage client fix as started today. Affected machines (including some sci machines) may need rebooting.  
For the time being, please refrain from submitting further helpdesk queries about the above issues, since some aspects of the plan are still to be implemented and may take some time to have the desired effect. However we will try and provide further updates over the following days.


Thank you for your patience and cooperation.


Best wishes,  
JASMIN team


