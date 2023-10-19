---
title: Tips to avoid problems accessing JASMIN/CEMS services
date: 2016-10-11 13:08:31+00:00
tags: ['news']
aliases: ['/blog/tips-to-avoid-problems-accessing-jasmincems-services']
thumbnail: 
icon: fas circle-info
---
With JASMIN/CEMS system now past its third anniversary, users will now start to encounter default access periods for their accounts. Users will be sent reminder emails to renew their access to our systems, but the following article provides advice to help avoid any issues which may cause common problems accessing JASMIN/CEMS services :


* Go to [myCEDA](https://services.ceda.ac.uk/cedasite/myceda/) and check that your email address and other details are up to date. This ensures that when we, or automated system messages attempt to contact you, we can be sure that messages will reach you.
* Your CEDA account only gives you certain privileges by default. As with CEDA archive datasets, most JASMIN services (including access to the login, science analysis servers and transfer machines, and individual Group Workspaces) require additional registration steps which expire after a default period (usually 3 years). You can check the validity period of all your current registrations at [myCEDA](https://services.ceda.ac.uk/cedasite/myceda/), and renew in advance to avoid any gaps in access.
* Typically, you will be emailed 3 months, 14 days and again 7 days before any registration expires, but the onus is on you to renew your registration for each service.
* If your registration for a "login" role expires, your SSH key will automatically be revoked from the relevant servers and you will be unable to log in, so login registrations are particularly important to keep up-to-date.
* Please avoid workflows which involve multiple SSH connections in quick succession (e.g. copying many very small files with individual scp commands). These can appear similar to "denial of service" attempts and can cause your account to be denied access for periods of time.


See also <http://help.ceda.ac.uk/article/276-tips-to-avoid-problems-accessing-jasmin-services>

