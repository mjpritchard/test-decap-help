---
title: JASMIN Migration to CentOS7 UPDATE 2
date: 2019-10-28 14:07:44+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-migration-to-centos7-update-2']
thumbnail: 
icon: fas circle-info
---
This is the second update about our progress towards updating our infrastructure from RedHat Enterprise Linux 6 (RHEL6) to CentOS7.


This was first announced here:   
<https://www.ceda.ac.uk/blog/migration-of-jasmin-virtual-machines-how-will-this-affect-you/>


Further details are provided here:  
<http://www.jasmin.ac.uk/articles/vm-migration/>


There are 2 main strands to this activity:  
1. Replacing the “JASMIN Analysis Platform” (JAP), the software stack deployed on both the JASMIN “sci” servers and LOTUS.  
2. Migrating virtual machines (VMs) used for hosting component services of JASMIN and CEDA, plus a small number of project-specific VMs.


This update will focus on (1), since (2) is now underway in a manner largely transparent to most users.


The JAP replacement takes the form of 2 new components:  
\* a new conda-based Python environment called Jaspy  
\* a Software Collections Library (SCL) which encapsulates the non-Python which were also part of the JAP.


Detailed documentation for Jaspy is available here: <https://help.jasmin.ac.uk/article/4729-jaspy-envs>


Documentation about the SCL is also being developed.


There are some further tests to carry out over the next couple of weeks, but both of these components are nearly ready for production deployment. Our current aim is to have the following available by MID-NOVEMBER 2019:  
\* A sample CentOS7 “sci” machine with JASPY available and the SCL installed  
\* A LOTUS queue with access to CentOS7 nodes set up the same as the CentOS7 “sci” machine


The next announcement will give details of how these resources can be accessed by users interested in testing their code/workflows against the new software stack.


Thank you for your attention and please look out for further updates as this work progresses.


CEDA and JASMIN Team

