---
title: Update on JASMIN issues 30 Aug 2023
date: 2023-08-30 14:34:54+00:00
tags: ['news']
aliases: ['/blog/update-on-jasmin-issues-30-aug-2023']
thumbnail: 
icon: fas circle-info
---

Further investigation of the storage and networking issues affecting CEDA and JASMIN services means that some additional interventions are required:

* All LOTUS batch cluster partitions have been paused - new jobs can still be submitted, but will not be scheduled until the cluster is healthy. Existing jobs will continue to run, but will remain at risk due to these issues.
* Some volumes e.g. `/apps/jasmin` and `/gws/smf/*` are still inaccessible from many hosts, so software under the “modules” system (including jaspy) are not available.
* Migration of data from the affected storage is now underway
* Faulty network switches are being replaced as soon as this has completed

This work will continue into tomorrow morning, so please note that systems are not expected to return to normal until later tomorrow morning Thursday 31st August. We will provide another update at that point.

With apologies for any inconvenience caused,

JASMIN Team
