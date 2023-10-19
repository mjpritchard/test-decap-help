---
title: Update to high-performance data transfer services
date: 2021-02-26 13:26:52+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/update-to-high-performance-data-transfer-services-1']
thumbnail: 
icon: fas circle-info
---

Dear users,


As previously announced, we are making further changes to some data transfer services:


* **ftp.ceda.ac.uk (CEDA Archive FTP server)**  
The new host for this service will operate at the same name ftp.ceda.ac.uk, but if you have used the hostname ftp2.ceda.ac.uk directly, then you are advised to change to using the alias ftp.ceda.ac.uk so that the change happens transparently to you when the old server is decommissioned.
* **JASMIN GridFTP Server Globus Endpoint**  
The Globus endpoint will change to a new server on Tuesday 2nd March. If you are using the “JASMIN GridFTP Server” Globus endpoint via Globus web or command-line interfaces, the endpoint ID of the service will remain the same but the server at the JASMIN end will change. This should only affect transfers in progress at the time of the change, so impact should be minimal given that this coincides with the planned maintenance day already announced.  
However, if you use certificate-based gridftp (gsiftp) directly i.e, **not** via Globus Online interfaces, but with the globus-url-copy client, then the hostname data-xfer1.ceda.ac.uk will need to be replaced with gridftp1.jasmin.ac.uk in your gsiftp:// URIs. All other aspects should remain the same.


We are still investigating an issue affecting transfers to and from some file system (particularly affecting transfers made using Globus) and this is still not yet fully resolved.


Please also note [the scheduled maintenance day coming up on 2nd March.](https://www.ceda.ac.uk/blog/advance-notice-jasmin-system-maintenance-tues-2-march-2021/)


JASMIN Team


