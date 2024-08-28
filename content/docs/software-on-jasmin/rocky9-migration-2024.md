---
description: Software and operating system changes - migration to Rocky Linux 9 (Summer 2024)
slug: rocky9-migration-2024
title: Migration to Rocky Linux 9 2024
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
Please find below details of the new Rocky 9 environment on JASMIN. We will update other documentation to match this in due course, but the information below will be the most up-to-date source until further notice.
{{</alert>}}

## Details of the new Rocky Linux 9 environment

### General

The move to Rocky Linux 9 (abbreviated to "Rocky9" or "R9" from here on) involves many changes at
lower levels transparent to users, so we will focus here on those most relevant to how services on 
JASMIN are accessed and used. The reasons for the choice of Rocky 9 itself, and for some of the
associated changes to software, machines and services provided, will not be covered in detail,
but have been influenced by a number of factors including:

- organisational security and maintenance policies
- availablity of packages and dependencies for the chosen operating system
- user feedback

### login nodes

The list of new login nodes is as follows:

name | status
--- | ---
`login-01.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} ready to use
`login-02.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} ready to use
`login-03.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} ready to use
`login-04.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} ready to use
{.table .table-striped .w-auto}

Notes:

- There is no longer any requirement for forward/reverse DNS lookup or any restriction by 
institutional domain. You no longer need to register non-`*.ac.uk` domains with the JAMSIN 
team (exception: {{<link "#hpxfer-servers">}}hpxfer{{</link>}})
- This means all users can access all login servers (previously some users could only use
 `login2`)
- As before, no filesystems other than the home directory are mounted.
- Use only as a "hop" to reach other servers within JASMIN.

### NX login nodes

name | status
--- | ---
`nx1.jasmin.ac.uk` | {{< icon fas square-xmark text-danger >}} Not yet ready: issue with Windows 11 clients
`nx2.jasmin.ac.uk` | {{< icon fas square-xmark text-danger >}} Not yet ready: issue with Windows 11 clients
`nx3.jasmin.ac.uk` | {{< icon fas square-xmark text-danger >}} Not yet ready: issue with Windows 11 clients
`nx4.jasmin.ac.uk` | {{< icon fas triangle-exclamation text-warning >}} Not yet moved to Rocky9 (works as previously for now)
{.table .table-striped .w-auto}

Notes:

- Nodes have identical configuration so no need for some users to only use certain nodes as before.
- By keeping the host names as short as possible, we mitigate the issue some users (with long
usernames created before the 8-character rule) had with agent forwarding: all should behave
the same as the old `nx4` in this respect.
- As before, no filesystems other than the home directory are mounted.
- Use only with the NoMachine NX graphical linux desktop, from where you can
  - use the Firefox browser on the linux desktop to access web resources only accessible within JASMIN
  - make onward connections to a sci server for using graphics-intensive applications
- Make sure you are using the most up-to-date version of 
{{<link "https://downloads.nomachine.com/download-enterprise/#NoMachine-Enterprise-Client">}}NoMachine Enterprise Client{{</link>}}.

### sci servers

We have introduced a new naming convention which helps idendify virtual and physical/high-memory sci servers.
The new list is as follows:

name | status | specs
--- | --- | ---
Virtual servers | | 
`sci-vm-01.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | (specs tbc)
`sci-vm-02.jasmin.ac.uk` | {{< icon fas triangle-exclamation text-warning >}} Finalising configuration | (specs tbc)
`sci-vm-03.jasmin.ac.uk` | {{< icon fas triangle-exclamation text-warning >}} Finalising configuration | (specs tbc)
`sci-vm-04.jasmin.ac.uk` | {{< icon fas triangle-exclamation text-warning >}} Finalising configuration | (specs tbc)
`sci-vm-05.jasmin.ac.uk` | {{< icon fas triangle-exclamation text-warning >}} Finalising configuration | (specs tbc)
`sci-vm-06.jasmin.ac.uk` | {{< icon fas triangle-exclamation text-warning >}} Finalising configuration | (specs tbc)
Physical servers | |
`sci-ph-01.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | (specs tbc)
`sci-ph-01.jasmin.ac.uk` | {{< icon fas circle-check text-success >}}Ready to use |  (specs tbc)
{.table .table-striped .w-auto}

Notes:

- For users within the STFC network, there is no longer any reverseDNS restriction, so all
should be accessible directly within that network without need to go via a login node.
- Replacements for common tools:
  - `lxterminal` has been replaced with {{<link href="https://docs.xfce.org/apps/terminal/start">}}xfce-terminal{{</link>}}
  - for a more richly-featured editor or Integrated Development Environment (IDE), users should consider using
   the remote editing features of {{<link href="https://code.visualstudio.com/docs/remote/ssh">}}VSCode{{</link>}} or 
   {{<link "https://www.jetbrains.com/pycharm/">}}PyCharm{{</link>}}, since these can be installed and customised locally
   by the user to their taste rather than needing central installation and management on JASMIN. Watch this space for
   further advice about how to configure and use VSCode in this way.
- See {{<link "#jaspy">}}jaspy{{</link>}}, {{<link "#jasr">}}jasr{{</link>}} and {{<link "#jasmin-sci">}}jasmin-sci{{</link>}}
sections below for further information on software.
- For graphical applications, use the {{<link "#nx-login-nodes">}}NoMachine NX service{{</link>}} rather than
sending X11 graphics over the network back to your laptop/desktop, to ensure performance.
- As before, physical servers are actually re-configured nodes within the LOTUS cluster and as such have different a network
configuration from the virtual `sci` servers, with limited outward connectivity.

### xfer servers

name | status | notes
--- | --- | ---
`xfer-vm-01.jasmin.ac.uk` | {{< icon fas square-xmark text-danger >}} Not yet ready | Virtual server
`xfer-vm-02.jasmin.ac.uk` | {{< icon fas square-xmark text-danger >}} Not yet ready | Virtual server
`xfer-vm-03.jasmin.ac.uk` | {{< icon fas square-xmark text-danger >}} Not yet ready | Virtual server, will have `cron`.
{.table .table-striped .w-auto}

### hpxfer servers

name | status | notes
--- | --- | ---
`hpxfer3.jasmin.ac.uk` | {{< icon fas square-xmark text-danger >}} Not yet ready | Physical server
`hpxfer4.jasmin.ac.uk` | {{< icon fas square-xmark text-danger >}} Not yet ready | Physical server
{.table .table-striped .w-auto}

### gridftp server

For users of certificate-based gridftp only (specifially, `gsiftp://` using the `globus-url-copy` client), there is a new server:

name | status
--- | ---
`gridftp2.jasmin.ac.uk` | {{< icon fas square-xmark text-danger >}} Not yet ready
{.table .table-striped .w-auto}

Notes:

- Make sure you are using `slcs.jasmin.ac.uk` as the short-lived credentials server, with your JASMIN
account credentials. CEDA identities can no longer be used for authentication with this server.
- We now encourage users of this service to migrate to use the {{<link "#globus-data-transfer-service">}}Globus service{{</link>}}
for data transfers. This older gridftp service will likely be decomissioned over the next 12 months.
- Use of `globus-url-copy` is nothing to do with the {{<link "#globus-data-transfer-service">}}Globus service{{</link>}}: they are now very separate things.

### Globus data transfer service

Where possible you should now use the Globus data transfer service for any data transfer in or out of JASMIN: this is now the recommended method,
which will get you the best performance & has a number of advantages over logging into a server and doing transfers manually.

As introduced earlier this year, the following Globus collections are available to all users of JASMIN, with no special access roles required:

name | uuid | status | notes
--- | --- | --- | ---
JASMIN Default Collection | `a2f53b7f-1b4e-4dce-9b7c-349ae760fee0` | {{< icon fas circle-check text-success >}} Ready to use | Best performance, currently has 2 physical Data Transfer Nodes (DTNs).
JASMIN STFC Internal Collection | `9efc947f-5212-4b5f-8c9d-47b93ae676b7` | {{< icon fas circle-check text-success >}} Ready to use | For transfers involving other collections inside the STFC network. 2 DTNs, 1 physical, 1 virtual. Can be used by any user in case of issues with the above collection.
{.table .table-striped .w-auto}

Notes:

- These collections can be used with the Globus {{<link "https://app.globus.org">}}web interface{{</link>}},
{{<link href="https://docs.globus.org/cli/">}}command-line interface (CLI){{</link>}}, or its {{<link href="https://globus-sdk-python.readthedocs.io/en/stable/">}}Python software development kit (SDK){{</link>}}, and use the JASMIN accounts portal for authentication

### Software

Please see the table below and accompanying notes which together summarise the upcoming changes to aspects of software on JASMIN:

Software | CentOS7 | Rocky 9
--- | --- | ---
IDL versions<br>IDL licence server<br>**see Note 1** | 8.2, 8.5 (D), 8.5, 8.6<br>Flexnet | 8.9, 9.0. (8.6?)<br>Next generation
Cylc<br>Cylc UI visualisation<br>**see Note 2**  | 7.8.14 and 8.3.3-1<br>UI functionality integrated | 8.3.3-1<br>UI via browser: discussion ongoing
Jaspy<br>Jasr<br>jasmin-sci | 2.7, 3.7 (all variants), 3.10 (all variants)<br>3.6, 4.0 (all variants), 4.2<br>URL page of the packages | 3.11<br>4.3<br>rpm/Glibc compatibility tba?
Intel compilers | 12.1.5-20.0.0 (11 variants) | Intel oneAPI
MPI library/ OpenMPI<br>versions/compiler<br>**see Note 3**  | 3.1.1/Intel,GNU, 4.0.0<br>4.1.[0-1,4-5]/Intel<br>4.1.2, 5.0.1, 5.1.2 | 4.1.5/Intel/gcc &  5.0.4 /intel/gcc<br><br>Possibility to support mpich or IntelMPI
NetCDF C library<br>NetCDF Fortran binding lib. | netcdf/gnu/4.4..7, netcdf/intel/14.0/<br>netcdff/gnu/4.4.7/*, netcdff/intel/4.4.7<br>parallel-netcdf/gnu/201411/22<br>parallel-netcdf/intel/20141122 | A new module env for serial and parallel version GNU and Intel oneAPI build of NetCDF against either OpenMPI and/or Intel MPI
GNU compilers | 7.2.0 ,8.1.0,  8.2.0<br>13.2.0 conda-forge (12.1.0 from legacy JASPY) | 11.4.1 (OS)<br>13.2.0 conda-forge via JASPY
JULES <br>**see Note 4**| | Information to follow
{.table .table-striped .w-auto}

#### Notes

1. **IDL:** We will not support IDL 8.5 & older versions on Rocky9 but we might continue to support IDL 8.6 if there is a need from the user community: we are still assessing that. The present version of IDL 8.6 must be migrated from the current "Flexnet" to the new "Next Generation" licensing system.
We obtained IDL 8.9 and IDL 9 from NV5 and are in the process to setup “Next Generation" licensing to activate the licence. Once this is done on server and client machines and testing is completed, a new module environment will be created users for IDL 8.9 and 9.0 on the new sci machines and a subset of the new LOTUS Rocky9 nodes. The default `module add idl` will then load IDL 8.9 instead of IDL 8.6.

2. **Cylc:** Note that Cylc 8 differs from Cylc7 in many ways: architecture, scheduling algorithm, security, UIs, working practices and more. The Cylc 8 web UI requires the use of a browser (e.g. Firefox in the NoMachine desktop service)

3. **MPI:** (further details to follow)

4. **JULES:** (further details to follow)


### Upgraded LOTUS cluster

Further information to follow.

### Other services

Further information to follow.