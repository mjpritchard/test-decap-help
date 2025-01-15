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

{{< alert color="success" icon="fas circle-exclamation" >}}
Lots of updated information below about the new Rocky Linux 9 environment on JASMIN: please read, and keep checking back here regularly for now.
{{</alert>}}

## Introduction

As with a previous migration completed in 2020, the change of operating system version is needed to make sure that the version in use is current and fully supported, i.e. that package updates are available and important security updates can be obtained and applied to keep the platform secure.

The current operating system, CentOS7 is officially end-of-life as of the end of June 2024. We will be moving from CentOS7 to Rocky Linux 9, which is supported until May 2032. Rocky 9 should provide a very similar user experience to that provided by CentOS7, but with more recent software packages. Some software may have been removed or replaced during this transition.

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

The move to Rocky Linux 9 (abbreviated to "Rocky 9" or "R9" from here on) involves many changes at
lower levels transparent to users, so we will focus here on those most relevant to how services on 
JASMIN are accessed and used. The reasons for the choice of Rocky 9 itself, and for some of the
associated changes to software, machines and services provided, will not be covered in detail,
but have been influenced by a number of factors including:

- organisational security and maintenance policies
- availability of packages and dependencies for the chosen operating system
- user feedback

### Login nodes

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
institutional domain. You no longer need to register non-`*.ac.uk` domains with the JASMIN 
team (exception: {{<link "#hpxfer-servers">}}`hpxfer`{{</link>}})
- This means all users can access all login servers (previously some users could only use
 `login2`)
- As before, no filesystems other than the home directory are mounted.
- Use only as a "hop" to reach other servers within JASMIN.
- **Make sure your SSH client is up to date**. Check the version with `ssh -V`. If
it's significantly older than `OpenSSH_8.7p1, OpenSSL 3.0.7`, speak to your local
admin team as it may need to be updated before you can connect securely to JASMIN.

### NX login nodes

name | status
--- | ---
`nx1.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} [Ready for use, update your SSH key]({{% ref "graphical-linux-desktop-access-using-nx#setting-up-your-connection" %}})
`nx2.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} [Ready for use, update your SSH key]({{% ref "graphical-linux-desktop-access-using-nx#setting-up-your-connection" %}})
`nx3.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} [Ready for use, update your SSH key]({{% ref "graphical-linux-desktop-access-using-nx#setting-up-your-connection" %}})
`nx4.jasmin.ac.uk` | {{< icon fas triangle-exclamation text-danger >}} Old server, closing soon [see retirement timetable](#timetable-for-host-retirements)
{.table .table-striped .w-auto}

Notes:

- [Updated advice for connection]({{% ref "graphical-linux-desktop-access-using-nx#setting-up-your-connection" %}}), requires updating your SSH key.
- New nodes have identical configuration so are accessible from all network locations (no further need for some users to use only certain nodes).
- By keeping the host names as short as possible, we mitigate the issue some users (with long
usernames created before the 8-character rule) had with agent forwarding: all should behave
the same as the old `nx4` in this respect.
- As before, no filesystems other than the home directory are mounted.
- Use only with the NoMachine Enterprise Client to get a graphical Linux desktop, from where you can
  - use the Firefox browser on the linux desktop to access web resources only accessible within JASMIN
  - make onward connections to a `sci` server for using graphics-intensive applications
- Make sure you are using the most up-to-date version of 
{{<link "https://downloads.nomachine.com/download-enterprise/#NoMachine-Enterprise-Client">}}NoMachine Enterprise Client{{</link>}}.

### `sci` servers

We have introduced a new naming convention which helps identify virtual and physical/high-memory `sci` servers.
The new list is as follows:

name | status | specs
--- | --- | ---
Virtual servers | | 
`sci-vm-01.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | 8 CPU / 32 GB RAM / 80 GB (virtual disk)
`sci-vm-02.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | 8 CPU / 32 GB RAM / 80 GB (virtual disk)
`sci-vm-03.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | 8 CPU / 32 GB RAM / 80 GB (virtual disk)
`sci-vm-04.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | 8 CPU / 32 GB RAM / 80 GB (virtual disk)
`sci-vm-05.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | 8 CPU / 32 GB RAM / 80 GB (virtual disk)
`sci-vm-06.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | 8 CPU / 32 GB RAM / 80 GB (virtual disk)
Physical servers | |
`sci-ph-01.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | 48 CPU AMD EPYC 74F3 / 2 TB RAM / 2 x 446 GB SATA SSD
`sci-ph-02.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} Ready to use | 48 CPU AMD EPYC 74F3 / 2 TB RAM / 2 x 446 GB SATA SSD
{.table .table-striped .w-auto}

Notes:

- For users within the STFC network, there is no longer any reverse DNS restriction.
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
  - X11 graphics functionality is still to be added to these machines (coming shortly), but currently this will fail with an error like:
    ```
    xterm: Xt error: Can't open display: 
    xterm: DISPLAY is not set
    ```
- As before, physical servers are actually re-configured nodes within the LOTUS cluster and as such have different a network
configuration from the virtual `sci` servers, with limited outward connectivity.

### `xfer` servers

name | status | notes
--- | --- | ---
`xfer-vm-01.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} ready to use | Virtual server
`xfer-vm-02.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} ready to use | Virtual server
`xfer-vm-03.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} ready to use | Virtual server, has `cron`.
{.table .table-striped .w-auto}

Notes:

- Similar config on all 3 (no domain or reverse DNS restrictions now)
- Same applies re. **SSH client version**, see [login nodes]({{% ref "#login-nodes" %}})
- If using cron on `xfer-vm-03`, you must use [crontamer]({{% ref "using-cron/#crontamer" %}})
- Throttle any automated transfers to avoid many SSH connections in quick succession, otherwise you may get blocked.
- Consider using [Globus]({{% ref "#globus-data-transfer-service" %}}) for any data transfer in or out of JASMIN
- A new software collection `jasmin-xfer` has now been added to these servers, providing these tools:

```txt
emacs-nox
ftp
lftp
parallel
python3-requests
python3.11
python3.11-requests
rclone
rsync
s3cmd
screen
xterm
```

### `hpxfer` servers

name | status | notes
--- | --- | ---
`hpxfer3.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} ready to use | Physical server
`hpxfer4.jasmin.ac.uk` | {{< icon fas circle-check text-success >}} ready to use  | Physical server
{.table .table-striped .w-auto}

Notes:

- Tested with `sshftp` (GridFTP over SSH) from ARCHER2
- Same applies re. **SSH client version**, see [login nodes]({{% ref "#login-nodes" %}})
- The software collection `jasmin-xfer` available as per [xfer servers, above]({{% ref "#xfer-servers" %}})
- `hpxfer` access role **no longer required for these new servers** (role will be retired along with the old servers in due course, so no need to renew if you move to the new servers)

### GridFTP server

Due to difficulties installing and configuring the suite of legacy components needed to support "old-style" gridftp, **we will not now be providing a replacement for the old server `gridftp1`**. Please familiarise yourself with using Globus, see below: this provides equivalent (and better) functionality.

Note this does affect gridftp-over-ssh (`sshftp`) which is available on the new `hpxfer` nodes in the same way as their predecessors, see above.

### Globus data transfer service

Where possible you should now use the Globus data transfer service for any data transfer in or out of JASMIN: this is now the recommended method,
which will get you the best performance and has a number of advantages over logging into a server and doing transfers manually.

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
IDL versions<br>IDL licence server<br>**see Note 1** | 8.2, 8.5 (D), 8.5, 8.6<br>Flexnet | 8.9, 9.1(D)<br>Next generation
Cylc<br>Cylc UI visualisation<br>**see Note 2**  | 7.8.14 and 8.3.3-1<br>UI functionality integrated | 8.3.3-1<br>UI via browser: discussion ongoing
Jaspy<br>Jasr<br>jasmin-sci | 2.7, 3.7*, 3.10* (*: all variants)<br>3.6, 4.0 (all variants), 4.2<br>URL page of the packages | 3.11<br>4.3<br>rpm/Glibc compatibility tba?
Intel compilers | 12.1.5-20.0.0 (11 variants) | Intel oneAPI
MPI library/ OpenMPI<br>versions/compiler<br>**see Note 3**  | 3.1.1/Intel,GNU, 4.0.0<br>4.1.[0-1,4-5]/Intel<br>4.1.2, 5.0.1, 5.1.2 | 4.1.5/Intel/gcc &  5.0.4 /intel/gcc<br><br>Possibility to support mpich or IntelMPI
NetCDF C library<br>NetCDF Fortran binding lib. | netcdf/gnu/4.4..7, netcdf/intel/14.0/<br>netcdff/gnu/4.4.7/*, netcdff/intel/4.4.7<br>parallel-netcdf/gnu/201411/22<br>parallel-netcdf/intel/20141122 | A new module env for serial and parallel version GNU and Intel oneAPI build of NetCDF against either OpenMPI and/or Intel MPI
GNU compilers | 7.2.0 ,8.1.0,  8.2.0<br>13.2.0 conda-forge (12.1.0 from legacy JASPY) | 11.4.1 (OS)<br>13.2.0 conda-forge via JASPY
JULES <br>**see Note 4**| | Information to follow
{.table .table-striped .w-auto}

#### Notes

1. **IDL:**
   1. IDL versions 8.9 and 9.1 are now available on the Rocky 9 sci servers.
   1. These will also be the versions available on the new cluster, which will be announced in early 2025.
   1. Licensing is now in place to enable use of these versions on Rocky 9 servers, in runtime or interactive mode.
   1. For the limited remaining time that the existing LOTUS cluster is available (with CentOS7 nodes), 8.5 is the default with other legacy versions still available on those nodes.

2. **Cylc:** Note that Cylc 8 differs from Cylc 7 in many ways: architecture, scheduling algorithm, security, UIs, working practices and more. The Cylc 8 web UI requires the use of a browser (e.g. Firefox in the NoMachine desktop service)

3. **MPI:** (further details to follow)

4. **JULES:** (further details to follow)

### Upgraded LOTUS cluster

Preliminary node specification:

type | status | specs
--- | --- | ---
standard | {{< icon fas triangle-exclamation text-warning >}} Available for testing | 190 CPU / 1.5 TB RAM / 480 GB SATA SSD + 800 GB NvMe SSD
high-mem | {{< icon fas triangle-exclamation text-warning >}} Available for testing | 190 CPU / 6 TB RAM / 480 GB SATA SSD + 800 GB NvMe SSD
{.table .table-striped .w-auto}

Notes:

- Overall ~55,000 cores: ~triples current capacity
- New nodes will form a new cluster, managed separately to the "old" LOTUS
- Submission to the new cluster will initially be via `sci-ph-03`, until **30 Jan 2025** when remaining physical sci nodes `sci-ph-0[1,2]` will be switched over to the new cluster.
  - and from **one** additional physical node (details TBC) with extended CentOS7 support, with restricted access to enable use of Cylc 7 for limited period.
- Submission to "old" LOTUS will **only** be from current CentOS7 `sci` machines `sci[1-8]` **until 18 Feb 2025**.
  - and from **one** additional physical node (details TBC) with extended CentOS7 support, with restricted access to enable use of Cylc 7 for limited period.
- Nodes will gradually be removed from the "old" cluster and retired, timetable TBC once new cluster is up & running.

### New LOTUS2 cluster initial submission guide

{{<alert type="info">}}
Please see the details below on how to access LOTUS2 and how to submit a job to the new Slurm scheduling partitions.

**These require a Slurm account, partition and quality of service (QoS) to be specified at job submission time**.
{{</alert>}}

#### LOTUS2 batch job submission host

Login to `sci-ph-03.jasmin.ac.uk`. The hostname will be displayed as `host1000`. This host can be reached in the normal way via a login server.

(Other submission hosts will be added in due course, see above)

#### New Slurm job accounting hierarchy

Slurm accounting by project has been introduced as a means of monitoring compute usage by projects on JASMIN. These projects align with group workspaces (GWSs),
and you will automatically be added to Slurm accounts corresponding to any GWS projects that you belong to.

To find what Slurm accounts and quality of services that you have access to, use the `useraccounts` command on the job submission host (currently `sci-ph-03.jasmin.ac.uk`).
Output should be similar to one or more of the lines below.

{{<command user="user" host="host1000">}}
useraccounts
(out)fred  mybiggws debug,highres,long,short,standard
(out)fred  jules-test jules-test
(out)fred  no-project debug,highres,long,short,standard
(out)fred  orchid debug,highres,long,short,standard
{{</command>}}

Users who do not belong to any group workspaces will be assigned the `no-project` account and should use that in their job submissions.

#### Partitions and QoS

There are 3 partitions currently available on LOTUS2, with associated allowed quality of service (QoS) as shown below:

| Partition | Allowed QoS |
| --- | --- |
| `standard` | `standard`, `short`, `long` |
| `highres` | `highres`, `reservation` |
| `debug` | `debug`, `reservation` |
{.table .table-striped .w-auto}

| QoS | Priority | Max CPUs per job | Max wall time |
| --- | --- | --- | --- |
| `standard` | 500 | 1 | 24 hours |
| `short` | 550 | 1 | 4 hours |
| `long` | 350 | 1 | 5 days |
| `highres` | 450 |  | 2 days |
| `debug` | 500 |  | 1 hour |
{.table .table-striped .w-auto}

#### Job submission

In order to successfully submit a job to LOTUS2, 3 mandatory fields must be specified. These are a partition, an account, and a QoS. The LOTUS2 configuration has been set to use the `standard` partition as the default if none is specified. However, users are discouraged from relying on this.

Example of a batch Script:

```bash
#!/bin/bash  
#SBATCH --job-name="Job Name" 
#SBATCH --time=<wall time required> 
#SBATCH --mem=<memory required> 
#SBATCH --cpus=<cpus required for multicores jobs e.g. MPI > 
#SBATCH --account=<account_name>  
#SBATCH --partition=<partition_name>  
#SBATCH --qos=<qos_name> 

# rest of script here
```

For a pseudo-interactive session on a LOTUS2 compute node:

{{<command user="user" host="host1000">}}
srun --account=cedaproc --qos=standard --pty /bin/bash
(out)srun: job 586 queued and waiting for resources
(out)srun: job 586 has been allocated resources
module li
(out)
(out)
(out)Currently Loaded Modules:
(out)1) idl/9.1
{{</command>}}

### Timetable for host retirements

Please find below a timetable of planned host retirements in line with our move to Rocky Linux 9. 

Please start moving your work **NOW**
so that any issues can be resolved and disruption minimized.

| Host    | retirement date |
| ---     | --- |
| Group A | |
| `cron1.ceda` aka `cron.jasmin`<br>`xfer3`<br>`nx-login[2,3]` | 21/11/2024 16:00 |
| Group B | 
| `nx4` aka `nx-login4` | 6/12/2024 16:00 |
| Group C |
| `xfer1`<br>`hpxfer1` - already shut down due to technical issue<br>`sci[1,2,4]`<br>`login[1,2]` | 6/12/2024 16:00 |
| Group D | |
| `xfer2`<br>`hpxfer2`<br>`sci[5,6,8]`<br>`login[3,4]`<br>`gridftp1`| 13/12/2024 16:00 |
{.table .table-striped}

All the hosts listed have new Rocky 9 equivalents described in the document above.
Please check back regularly to keep up to date with this schedule.
