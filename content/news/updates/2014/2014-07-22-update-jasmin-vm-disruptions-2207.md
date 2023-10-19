---
title: Update JASMIN VM disruptions 22/07
date: 2014-07-22 09:33:13+00:00
tags: ['news']
aliases: ['/blog/update-jasmin-vm-disruptions-2207']
thumbnail: 
icon: fas circle-info
---
Following a hardware failure on one of the pair of disk arrays which housing the JASMIN virtual machine (VM) images over the weekend, the SCD team supporting the JASMIN infrastructure have managed to recover most VM images from the array, with the result that most affected VMs are now back up and running.


Those still offline are listed at the end of this email and will hopefully be restored in the next 1-2 days


However, please note the following:  
- some services may not have automatically restarted on some machines. CEDA is in the process of checking this where possible, but please contact the CEDA helpdesk if you come across any remaining issues.  
- all VM images are temporarily being served from the other disk array in the pair, with the result that some loss of performance & responsiveness may be experienced by users in the short term.  
- replacement hardware is on site already and, when operational, JASMIN VM images will be migrated back to their original location. In most cases this migration will be transparent to users, but it may be necessary for short downtimes on particular VMs to complete this. After migration, performance & responsiveness should return to normal.  
- As a result, VMs and the services they run should be considered "at risk" for at least the next 48 hours or until further updates are given.


CEDA and SCD would like to apologise for the inconvenience caused by this disruption.


  
Unavailable VMs at present:  
Priority servers:  
et1-test.ceda.ac.uk  
fatcat-test.jc.rl.ac.uk  
ftp-test.ceda.ac.uk  
ingest1-test.ceda.ac.uk  
jasmin-name-dev.ceda.ac.uk  
jasmin-xfer1-dev.ceda.ac.uk  
jasmin-xfer1-test.ceda.ac.uk  
web-dev1.ceda.ac.uk  
web-test1.ceda.ac.uk  
   
NON-PRIORITY servers:  
jasmin-sci1-dev.ceda.ac.uk  
pa-test.jc.rl.ac.uk  
pm-dev.jc.rl.ac.uk  
jasmin-sci2.ceda.ac.uk  
jasmin-sci1-test.ceda.ac.uk  
perfsonar-vm01.jc.rl.ac.uk

