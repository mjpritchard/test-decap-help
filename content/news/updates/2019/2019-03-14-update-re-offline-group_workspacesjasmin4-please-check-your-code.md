---
title: Update re. offline /group_workspaces/jasmin4/ - please check your code!
date: 2019-03-14 16:12:50+00:00
tags: ['news']
aliases: ['/blog/update-re-offline-group_workspacesjasmin4-please-check-your-code']
thumbnail: 
icon: fas circle-info
---
The following group workspaces are still offline:  
/group\_workspaces/jasmin4/


This downtime is caused by a bug in the storage that the GWS’s are hosted on. The error is triggered by the use of parallel writes within the GWS. The SOF storage that the GWS’s are located on do not allow use of parallel writes; please refer to the documentation here for guidance about how to avoid using parallel writes within the new GWS’s: <https://help.jasmin.ac.uk/article/4700-understanding-new-jasmin-storage>.


We are working on the issue and will provide further updates when available. In the meantime, please check that your code is not running parallel writes. 


Apologies again for any inconvenience caused.  
JASMIN team

