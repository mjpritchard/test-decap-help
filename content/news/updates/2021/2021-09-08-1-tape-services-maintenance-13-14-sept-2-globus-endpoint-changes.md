---
title: 1) Tape services maintenance 13-14 Sept, 2) Globus Endpoint changes.
date: 2021-09-08 13:03:06+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/1-tape-services-maintenance-13-14-sept-2-globus-endpoint-changes']
thumbnail: 
icon: fas circle-info
---

Dear users


Please note the following JASMIN updates:


**1) Tape services maintenance 13-14 September**


Tape services including Elastic Tape and the Near-Line Archive service will be unavailable due to system maintenance/upgrade work on 13th & 14th September. User recalls and ingest of data will be stopped at 12:00 on Monday 13th September ahead of maintenance work on Tuesday 14th September.


**2) Globus endpoint changes**


For JASMIN users of the Globus data transfer service: a new endpoint named “JASMIN Globus endpoint (jasmin credentials)” (ID=2b0a1a4c-ee1f-11eb-b467-eb47ba14b5cc) has been created. This now works with your JASMIN account credentials (the same as those which you use to log in to the JASMIN Accounts Portal).  
The old endpoint, now re-named “JASMIN Gridftp server (ceda credentials)” (ID=4cc8c764-0bc1-11e6-a740-22000bf2d559), is still operational for now but will be deprecated over the next few weeks (further announcement to follow).  
If you use Globus for your data transfers to/from JASMIN, please try using the new endpoint. Unfortunately the underlying [issue with some Globus transfers](https://help.jasmin.ac.uk/article/4998-issue-affecting-data-transfers-using-globus-online) remains unresolved for now.  
Transfers over gridftp via SSH authentication (for example from ARCHER2) are unaffected by this change.


Thank you in advance for your cooperation and apologies for any inconvenience caused.


JASMIN Team


