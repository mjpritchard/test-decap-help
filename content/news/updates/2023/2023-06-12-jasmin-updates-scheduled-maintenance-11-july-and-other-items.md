---
title: JASMIN updates Scheduled maintenance 11 July and other items
date: 2023-06-12 08:19:54+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-updates-scheduled-maintenance-11-july-and-other-items']
thumbnail: 
icon: fas circle-info
---

Dear users

Please note the following items for your attention:

1. JASMIN Regular scheduled maintenance day: 11 July 2023
2. New NX server available
3. Reboot of gws-access service  Tuesday 13th June 08:30 & future changes to service.

Details:

1. Regular scheduled maintenance day: 11 July 2023

    On a (roughly quarterly) basis, important updates are applied to systems within the JASMIN infrastructure (which also hosts the CEDA Archive and associated services) in order to keep them up to date and secure. Servers may need to be rebooted in order for these changes to take effect, so there may be an interruption to JASMIN and CEDA services on this date.

    The LOTUS batch processing cluster will be unavailable for the duration of the work on the day, to avoid running jobs being adversely affected. A reservation will start at **05:00 AM** on the day, and any job submitted before that with a running time that goes over the reservation period will not start until after the reservation has finished.

2. Additional NX server now available: nx-login4

    An additional NX server has been added to the NoMachine graphical desktop service. This server, **nx-login4.jasmin.ac.uk** shares the same network configuration as the other servers nx-login[23] so is available from anywhere (no reverse DNS required), but has the additional feature that it should work for users with longer usernames (greater than 8 characters). If you have had problems previously with agent forwarding (i.e. making an onward connection to other machines with NX), then you should try this machine to see if that solves the problem for you. Some users with very long usernames (created before a rule was introduced to limit them!) may still experience issues: please contact the helpdesk if this is the case.

    See <https://help.jasmin.ac.uk/article/4810-graphical-linux-desktop-access-using-nx>

3. Reboot of gws-access.jasmin.ac.uk server planned for  Tuesday 13th June 08:30

    (mainly for GWS managers who expose their GWS data via HTTP)

    This server, which provides HTTP access to public data files in group workspaces, will need to be rebooted at Tuesday 13th June 08:30 which will cause a brief interruption to that service.

    **NB**. Within the next few months we are preparing to move this service over to a new technology, which will take over the service at the same URL in due course. If your GWS currently exposes data via the existing service at <https://gws-access.jasmin.ac.uk>, please try out the alternative form of the service which is now (temporarily) available at the URL https://gws-access-xp.jasmin.ac.uk and let us know if anything does not work (note some absolute URLs may not work in this temporary form). Please also look out for further announcements about the future of this service.

Please plan your work accordingly to minimise any inconvenience caused.

Thank you for your attention.

Best wishes,

JASMIN Team
