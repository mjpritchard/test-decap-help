---
title: Network maintenance completed successfully!
date: 2016-10-07 15:13:59+00:00
tags: ['news']
aliases: ['/blog/network-maintenance-completed-successfully']
thumbnail: 
icon: fas circle-info
---
 

Maintaining, upgrading and continually preparing for the future developments of world class data analysis infrastructure for the environmental research community is an essential part of CEDA's ongoing service. This week saw the successful completion of a major system upgrade by our dedicated systems team, paving the way for the future of CEDA's JASMIN infrastrucutre.


Our system team worked a very long and intense day on Wednesday, the culmination of several months of planning to ensure that disruption was kept to a minimum and that the JASMIN core network is kept trouble-free. It was the first such scheduled downtime since February 2015.


Jonathan Churchill and his team of Cristina del Cano Novales and Ian Wester in STFC's Scientific Computing Department were joined by Stas Rudashevsky, tech support from network equipment supplier Mellanox, who flew in specially from Israel to ensure everything went smoothly, and Linda Edmondson from Panasas who provided valuable remote support from California to bring a large part of the storage back online. World wide support indeed for a world leading infrastructure!


{{< image src="/img/news/2016/2016-10-07-network-maintenance-completed-successfully/rack_2_small.jpg"  caption="Fast iSCSI and NetApp replacement" class="rounded" >}}The work focussed on essential firmware upgrades on 28 Mellanox 10/40Gb network switch/routers (about half of the infrastructure) to fix ~3 critical bugs which had required workarounds for the past 18 months.   
 Each switch required 3 upload, install and reboot cycles of about 1 hour each. The other half of the infrastructure had been upgraded transparently to users in the run up to the downtime.


{{< image src="/img/news/2016/2016-10-07-network-maintenance-completed-successfully/cables_small.jpg"  caption="Multi Terabits per Second cableing" class="rounded" >}}These switch/routers connect all the Panasas storage, the cloud infrastructures and around 1000 virtual and physical machines, so this work required careful planning and sequencing to take all dependancies into account, as the devices form a dynamic fabric which reacts to heal any changes.


{{< image src="/img/news/2016/2016-10-07-network-maintenance-completed-successfully/rack_1_small.jpg"  caption="New Dell server blades" class="rounded" >}}As a result of the upgrades we now have stable redundant routers for the VM block storage and hence able to release the small fast iSCSI storage which we hope will improve relational database performance, and the replacement system for our 3 yr old NetApp in time for its end of life in December. The upgrade has also stabilised the dynamic routing algorithms, (important as there are ~1,000 ethernet routes inside JASMIN !) allowing us to grow the network - eg to add the additional 1,000 cores to LOTUS and our Object storage . In addition the upgrade will allow us to move forward with our VXLAN support allowing us to grow the size of the JASMIN cloud networks transparently to users, as well as introduce management and Software Defined Networking (SDN) tool (Mellanox's NEO) to help us with our migration to OpenStack.


This bespoke high-performance network is one of the key features of JASMIN which makes it a world-class infrastructure for large-scale environmental science. Presentations given at the [recent JASMIN Conference](http://www.jasmin.ac.uk/jasmin-users/events/jasmin-conference-2016/ "Read more details about JASMIN at the recent JASMIN conference") provide more information about the range of science being undertaken and the innovative approaches enabled by JASMIN.


We would like to thank all involved for ensuring that the work went smoothly, and you, our user community for your understanding and patience while this essential work was carried out.


All systems should now be running as normal, but if you have found any new issue, please report any problems to our helpdesk at: support@ceda.ac.uk.


 


CEDA / JASMIN Team



 