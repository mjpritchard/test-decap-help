---
title: JASMIN Migration to CentOS7 UPDATE 3
date: 2019-12-11 09:47:37+00:00
tags: ['news']
aliases: ['/blog/jasmin-migration-to-centos7-update-3']
thumbnail: 
icon: fas circle-info
---

**This is the third update about migrating the JASMIN infrastructure from RedHat Enterprise Linux 6 (RHEL6) to CentOS7.**


The previous two announcements are linked here:  
[1st update](https://www.ceda.ac.uk/blog/migration-of-jasmin-virtual-machines-how-will-this-affect-you/) (Posted: 01/10/2019)    
[2nd update](https://www.ceda.ac.uk/blog/jasmin-migration-to-centos7-update-2/) (Posted: 28/10/2019) 


Further details can be found [here](http://www.jasmin.ac.uk/articles/vm-migration/).


**There are 2 main strands to this activity:**


1)    Replacing the “JASMIN Analysis Platform” (JAP), the software stack deployed on both the JASMIN “sci” servers and LOTUS.


2)    Migrating virtual machines (VMs) used for hosting component services of JASMIN and CEDA, plus a small number of project-specific VMs.


This update focuses on item (1). In parallel, we are working on (2), which will happen in a manner largely transparent to most users.


The JAP replacement takes the form of 2 new software components:


* a new Conda-based set of Python environments: known as "Jaspy"
* a Software Collections Library (SCL) which encapsulates the non-Python which were also part of the JAP: known as "jasmin-sci"


It is important that all users consider how this change might affect their workflows so we invite you to test the new CentOS7 systems and the software environments being provided. The machines available for testing are:


* A "sci" server:  jasmin-sci7-test.ceda.ac.uk
* A cluster of LOTUS nodes, available via the queue: "centos7"


We have drafted documentation about the changes to software on JASMIN. The documentation is currently provided as a single web-based document (PDF). Please review the documentation [here](https://drive.google.com/file/d/1gD9C0TZyNITibgDhlv3pRzgd4JjzVfBW/view?usp=sharing ).



Please let us know about your experience of using the CentOS7 machines, by e-mailing [CEDA Support](mailto:support@ceda.ac.uk) and including "centos7 support" in the subject line. Please send us both your positive and negative feedback so that we can gauge the response and react to problems. If you have any specific feedback regarding the documentation then please let us know.



**Next steps:**


In early January we will review the user feedback and make any necessary changes. Assuming there are no major issues we will then publicise a timetable for a gradual transition of all "sci" servers and LOTUS queues to CentOS7.



Thank you for your attention and please look out for further updates as this work progresses.


CEDA and JASMIN Team


