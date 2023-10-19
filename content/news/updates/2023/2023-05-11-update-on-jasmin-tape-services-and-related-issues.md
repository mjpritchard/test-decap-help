---
title: Update on JASMIN tape services and related issues
date: 2023-05-11 11:29:53.996436+00:00
tags: ['news', 'Elastic Tape']
aliases: ['/blog/update-on-jasmin-tape-services-and-related-issues']
thumbnail: 
icon: fas circle-info
---

Please note the further updates below:

* Although initially thought to be only a problem with ET/JDMA service itself, the current issues with slow throughput are now thought to be mainly due to a problem with the PFS storage from where the particular tape jobs are being ingested.
* The issue with PFS storage is also affecting other volumes in that system, including XFC volumes `/work/xfc/*`, and `/work/scratch-pw*` and `/gws/pw/j07/*`.
* These issues are being actively pursued with the storage vendor and the urgency has been escalated.
* Further interventions to restore stability to the tape services are possible in due course.

We apologise for the disruption caused by these issues, but are working to understand and resolve them as soon as possible.JASMIN Team.
