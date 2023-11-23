---
title: CEDA / JASMIN latest improvements 
date: 2023-11-23 10:00:00+00:00
tags: ['news', 'jasmin','ceda']
thumbnail: 
icon: fas paper-plane text-info
---

During the recent CEDA/JASMIN downtime we took the opportunity to make a range of changes, mostly behind the scenes, to make things more resilient and roll out a few enhancements. We’ve rounded these up here to share with our communities, to show how we made the best of the inevitable disruption to make improvements which benefit our user communities and ourselves in our day-to-day operations.

### CEDA sites

To ensure we remained visible during this period, and to improve resilience overall, we migrated a range of our sites away from hosting on JASMIN to external, cloud-based platforms. The new deployments have fewer moving parts and provide better content control and security, but crucially remain online when local issues occur, to help keep our user community up-to-date with developments at CEDA.

In particular, we rolled out a new-look site at: www.ceda.ac.uk. This includes the integration of a service-wide search feature to search across all CEDA sites, plus an improved presentation of news items and a new status page tracking current and future incidents.

{{< image src="/img/news/2023/2023-11-23-ceda-jasmin-latest-improvements/ceda-site.jpg"  caption="The new front page of the CEDA website" class="rounded" >}}

We also ported our main front page for the CEDA Archive site (archive.ceda.ac.uk) and CEDA Artefacts service (artefacts.ceda.ac.uk) to cloud-hosted services.

{{< image src="/img/news/2023/2023-11-23-ceda-jasmin-latest-improvements/artefacts-service.jpg" class="rounded" >}}

### Data Catalogue sites

With more citations in the literature for our datasets, it is important that related catalogue entries (especially our DOIed datasets) remain online. To ensure this, we prepared our catalogue service for deployment within the cloud, creating a more resilient service in the long run. We also released the first step towards improved record-to-record connectivity and searchability by embedding search within catalogue records to deliver filtering options to large dataset collections such as the FAAM aircraft dataset collection.

These improvements have reduced service load, improved rendering times for records and provided a more stable catalogue service for users as a result.

We also moved NERC’s central data catalogue (data-search.nerc.ac.uk) to a ‘containerised’ deployment. This makes more efficient use of resources and means that we can more readily redeploy this service, initially into the cloud during the JASMIN downtime, but now within our existing infrastructure whilst we seek a longer-term, more resilient option.

{{< image src="/img/news/2023/2023-11-23-ceda-jasmin-latest-improvements/catalogue-faam-flights.jpg" class="rounded" >}}

### JASMIN Improvements

Though JASMIN itself was offline for a number of days, we took the opportunity to carry out a number of essential tasks to minimise future service interruptions. The main one of these was upgrading Slurm to roll out important security updates. Meanwhile, our infrastructure team worked diligently behind the scenes to ensure a smooth shutdown and restart of the many subsystems which JASMIN and CEDA services depend on. Additionally, they undertook a number of hardware maintenance tasks to ensure the smooth running of the service.

### Other CEDA Work

Key database services were updated to maintain secure operation and minimise future interruptions.

CEDA staff also worked on a raft of other developments that are in the pipeline and hopefully should be rolled out in the coming months.

Meanwhile, the CEDA and JASMIN teams continue to review the impact of the downtime from several perspectives, to help improve advice, resilience and service delivery to our user communities.
