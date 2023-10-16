---
categories:
  - jasmin
date: 2021-02-01 15:35:52+00:00
title: Update to high-performance data transfer services
---


Dear users,

You will be aware that many JASMIN and CEDA services were redeployed from RHEL6 to CentOS7 operating systems last year. The final few services - those deployed on physical servers in the JASMIN Data Transfer Zone - are now nearly ready for user access, so please note the following if you make use of these services:

**jasmin-xfer[23].ceda.ac.uk** (high-performance data transfer servers)  

- now replaced by hpxfer[12].jasmin.ac.uk: please start using these instead.

-hpxfer1 has been available for several months, but now that hpxfer2 is also available, the old servers jasmin-xfer[23].ceda.ac.uk will be decommissioned on 12/02/2021.  
  
**ftp.ceda.ac.uk** (CEDA Archive FTP server)  
The new host for this service will operate at the same name ftp.ceda.ac.uk, but if you have used the hostname ftp2.ceda.ac.uk directly, then you are advised to change to using the alias ftp.ceda.ac.uk so that the change happens transparently to you when the old server is decommissioned on 12/2/2021.

**data-xfer1.ceda.ac.uk** (“JASMIN GridFTP Server” Globus Endpoint)  
This service has a new equivalent which will now be tested and will come into operation at a date to be announced in due course. The new host will be at a different hostname and will have a new Globus endpoint ID: details to follow once testing is complete.  
  
Please look out for further announcements.

JASMIN Team
