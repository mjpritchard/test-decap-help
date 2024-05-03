---
description: Software and operating system changes - migration to Rocky Linux 9 (Summer 2024)
slug: rocky9-migration-2024
title: Miration to Rocky Linux 9 2024
tags:
- centos7
- rocky9
- jaspy
- jasmin-sci
---

{{<alert type="info">}}
Watch this space for further updates about the details and timetable for the migration to Rocky Linux 9 on JASMIN.
{{</alert>}}

## Introduction

As with a previous migration completed in 2020, the change of operating system version is needed to make sure that the version in use is current and fully supported, i.e. that package updates are available and important security updates can be obtained and applied to keep the platform secure.

The current operating system, CentOS7 is officially end-of-life as of the end of June 2024. We will be moving from CentOS7 to Rocky Linux 9, which is supported until May 2032. Rocky9 should provide a very similar user experience to that provided by CentOS7, but with more recent software packages. Some software may have been removed or replaced during this transition.

This change affects JASMIN and CEDA services in several ways, including but not limited to the following:

- Components of all CEDA Archive and JASMIN web-based services need to be redeployed
- User-facing service hosts (e.g. `login`/`sci`/`xfer` and LOTUS nodes) all need to be redeployed
- All of these hosts need appropriate versions of drivers for various hardware and infrastructure components (e.g. storage, network, …) to be configured.
- The Slurm scheduler used for the LOTUS and ORCHID clusters needs to be adapted to work under Rocky 9, in terms of its own management functions and the worker nodes which it controls. A separate announcement will cover the expansion of LOTUS with new processing nodes: these will be introduced as a new cluster under Slurm, with existing nodes moved from old to new as part of the transition. There will be a limited window in which the 2 clusters will co-exist, during which time the old cluster will shrink in size: the current estimate for this is between July to September 2024, but we will provide updates on this as the new hardware is installed and timescales become clearer. We will endeavour to provide sufficient overlap and temporary arrangements to help users to migrate their workflows.
- Software made available centrally via the `module` system and under `/apps` needs to be made available in versions compatible with Rocky 9. Some software may need to be recompiled.
- Other software (e.g. run by users or groups, without being centrally managed) may need to be tested and in some cases recompiled in order to work correctly under Rocky 9.
- Management and monitoring systems need to be updated to operate in the new environment
- For tenants of the JASMIN Cloud, you should already be aware of our plans to move to use the STFC Cloud as the base platform for the JASMIN Cloud Service. Images are currently in preparation so that new (empty) tenancies will soon be available for tenants to manage the migration of their own virtual machines over to new instances using Rocky 9 images. It is anticipated at this stage that managed tenancies (with tenancy sci machines) will be discontinued as part of this move, so users of those VMs will be advised to use the new Rocky 9 general-use sci servers instead.

Much of this work is already underway by teams in CEDA and STFC’s Scientific Computing Department. As a result of extensive work by these teams in recent years to improve the way services are deployed and managed, we are now in a much better position to undertake this kind of migration with as little disruption to users as possible. Some disruption and adaptation by users will be inevitable, however.

Some services have already been migrated and are already running under Rocky 9, but there is still much work to be done over the coming weeks so please watch this space as we do our best to keep you informed of the progress we’re making, and of any actions you may need to take to minimise disruption to your work on JASMIN.

{{<alert type="info">}}
Further details to follow soon.
{{</alert>}}