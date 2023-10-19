---
title: Update on JASMIN maintenance Tues 31 Jan 2023 - window extended
date: 2023-01-31 16:55:46+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/update-on-jasmin-maintenance-tues-31-jan-2023-window-extended']
thumbnail: 
icon: fas circle-info
---

Scheduled maintenance work today has progressed well but some tasks will require extending the maintenance window into tomorrow Wednesday 1st February 2023.

* Parallel File System (PFS) Storage
* A second phase of the upgrade will hopefully be attempted early tomorrow morning but may need to be completed in working hours. This affects some CEDA Archive services, group workspaces with `/gws/pw/j07` paths and XFC (transfer cache) volumes
* LOTUS batch processing cluster: a reservation will remain in place until noon tomorrow, pending further updates.
* Some host upgrades may still be in progress, notably:
* CEDA FTP server and some CEDA Archive service hosts, hpxfer, and gridftp/Globus nodes
* Cloud
* VIO7 cloud platform is now working, external cloud OK but some individual machines may need checking by cloud tenants and rebooting. If problems persist please contact the helpdesk.
* Some archive/catalogue services are affected by an ongoing issue with the ElasticSearch database.
* Other service virtual machines (VMs) are now stable after yesterday’s issues: reboots as part of patching process should have fixed these so please report any issues with particular hosts to the helpdesk.

In summary: while many systems are back in operation, there is more work to be completed so in order to avoid disruption to their work, users are advised to avoid resuming work on the system until further notice tomorrow.

With apologies for any inconvenience caused.

Best wishes,
JASMIN Team
