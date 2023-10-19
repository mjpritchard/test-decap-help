---
title: Reminder - JASMIN planned maintenance and updates - Tuesday 18th October
date: 2022-10-14 08:56:02+00:00
tags: ['news', 'jasmin']
aliases: ['/blog/jasmin-planned-maintenance-and-updates-tuesday-18th-october']
thumbnail: 
icon: fas circle-info
---

Dear users,  
  



Please note the upcoming maintenance work affecting JASMIN on Tuesday 18th October. The following system work/enhancements are also planned for that date in order to minimise disruption: 


1. PFS storage update
2. Moving "/apps/contrib/" contents (early testing advised)
3. Slurm controller upgrade
4. Updates to software environments (jaspy, jasr, jasmin-sci)
5. Updates to the JASMIN Notebook Service (git and bash integrations)
6. Reboot external cloud/DTZ firewall
7. Update to JASMIN T&Cs & Privacy Policy


Details:  
  



1. **PFS storage update**  
Servers and clients of the parallel file system (PFS) storage will be updated. This should solve current issues with the PFS disk space usage reporting utility *pan\_df.*



2. **Moving "/apps/contrib/" contents (early testing advised)**


Software and applications under the partition */apps/contrib* (beat, snap, NAG & other libraries) will be migrated to a new area under */apps/jasmin*. Other applications and utilities e.g. compilers will be migrated  to a different storage system, but the mount points will remain the same.


The host *sci7.jasmin.ac.uk* is now available for users to test their workflows against these migrated software dependencies: users are encouraged to do this prior to the rollout date of 18th October, and are asked to report back any issues encountered.



3. **Slurm controller upgrade**


As part of the continuous improvement to the Slurm scheduler, the Slurm controller (slurmctld - the central resource manager) will be deployed on a new physical machine with a fast SSD disk. This will allow a better I/O throughput for intermediate Slurm state files.



The LOTUS batch processing cluster will be unavailable for the duration of the work on the day, to avoid running jobs being adversely affected. **A reservation will start at 05:00 am on 18th October** **on the day,** but any job submitted before 05:00 am with a running time that goes over the reservation period will not start until after the reservation has finished.



**IMPORTANT****:** No jobs will be accepted by SLURM from  **05:00 am on 18th October** until the reservation is lifted. Any attempt to submit a job to SLURM will be rejected with the following message: 


*sbatch: error: Batch job submission failed: Required partition not available (inactive or drain)*



4. **Updates to software environments (jaspy, jasr, jasmin-sci)**


The following software environments will have new default versions at **09:00 on 18th October:**


* *jaspy*: Python, and other, tools and libraries.
* *jasr*: R tools and libraries.
* *jasmin-sci*: other tools installed via RPMs



The new *jaspy* software environment will be available on the sci machines, LOTUS and Notebook Service (see below). The new release includes updates to a number of software packages as well as some new tools. The release, labelled as "*jaspy/3.10/r20220721*" is described on our Help Page at: <https://help.jasmin.ac.uk/article/4729-jaspy-envs>.



The new *jasr* software environment, labelled as "*jasr/4.0/r20220729*", will be released at the same time and is also described at the link above.



To test the new environments on the "sci" servers or LOTUS, use:



*module load <release\_label>*



**After 09:00 on 18th October the above releases will be the default versions of these software environments.** Once the switch has happened, you can activate the new *jaspy* or *jasr* release by typing:  



 *module load jaspy # for jaspy* *module load jasr  # for jasr*



Note that the previous *jaspy* release will continue to be available by using its full  label: "*jaspy/3.8/r20211105*".



Update to the *jasmin-sci* software packages will also be released on 18th October.



**IMPORTANT note for NCO/NCL users:**



We will be removing support for NCO and NCL from *jaspy* and adding these to *jasmin-sci* instead, so in order to continue to use these packages you will need to use “*module load jasmin-sci*” (in addition to loading the jaspy module if required for other packages).  In the event that you load both the *jasmin-sci* module and also the module for an older version of *jaspy* which still provides these packages, the module loaded last will take priority, so the ordering may affect which package version will run.



5. **Updates to the JASMIN Notebook Service (git and bash integrations)**


The following updates will be made available on the JASMIN Notebook Service (<https://notebooks.jasmin.ac.uk>):


* Python software kernel: updated to match the latest version of *jaspy* (see above).
* Integration with Git: the left-hand panel includes a Git button to enable interaction with remote repositories within the Jupyter environment.
* Terminal window: a Bash terminal window can now be run from within the Jupyter environment inside your browser.



6. **Reboot ext cloud/DTZ firewall**


A reboot of the external cloud firewall is scheduled in the morning on **Tuesday 18th October**. Access to the external cloud tenancies will be unavailable during that time.  



7. **Update to JASMIN T&Cs & Privacy Policy**


Some changes have recently been made to the JASMIN Terms and Conditions and Privacy Policy. Please make sure you have read, agree to and abide by these in your use of JASMIN. Links to these can be found in the footer of every JASMIN web-based service and on the JASMIN website, specifically:


<https://accounts.jasmin.ac.uk/account/conditions/><https://accounts.jasmin.ac.uk/account/privacy/>


On a regular (roughly quarterly) basis, important updates are applied to systems within the JASMIN infrastructure (which also hosts the CEDA Archive and associated services) in order to keep them up to date and secure. Servers may need to be rebooted in order for these changes to take effect, so there may be an interruption to JASMIN and CEDA services on this date.



**On this occasion, due to the nature and extent of the work being carried out, users will not be able to access JASMIN for large parts of the day. This affects the LOTUS batch processing cluster, significant parts of JASMIN storage, and many virtual machines on which services may be running.**



We advise you to plan your work accordingly to minimise the impact, but please accept our apologies in advance for any inconvenience.  
  



Thank you for your attention.  
  



Best wishes,  


JASMIN Team


 


