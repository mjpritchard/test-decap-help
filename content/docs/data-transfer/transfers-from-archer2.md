---
aliases: /article/4997-transfers-from-archer2
description: Transfers from ARCHER2
slug: transfers-from-archer2
title: Transfers from ARCHER2
---

## Choice of available Tools/Routes

See [Data Transfer Tools]({{% ref "data-transfer-tools" %}}) for general
details.

Users transferring data between ARCHER2 and JASMIN are often transferring
relatively large sets of data, so it is important to choose the most
appropriate route, method and tools to ensure you get the most efficient and
reliable transfer experience. This can vary depending on system and network
conditions.

The recommended option (as of mid-2024) is now **Globus**.

Common requirements to all of the methods are:

- an account with the [jasmin-login](https://accounts.jasmin.ac.uk/services/login_services/jasmin-login/) access role on JASMIN.
- a login account at ARCHER2

Please note:

- Enquiries about access to or use of ARCHER2 should be directed to ARCHER2 support ([support@archer2.ac.uk](mailto:support@archer2.ac.uk))
- Enquiries about access to or use of JASMIN should be directed to JASMIN support (use beacon, below-right or [support@jasmin.ac.uk](mailto:mailto:support@jasmin.ac.uk))

## Available transfer methods

### Basic SSH transfer

[**scp/rsync/sftp**]({{% ref "rsync-scp-sftp" %}}): Simple transfers using easy method, pushing data to general purpose xfer nodes. Convenient, but limited performance. 

_source_ |  _dest_ |  _notes_  
--- | --- | ---
`login.archer2.ac.uk` |  `xfer-vm-0[123].jasmin.ac.uk` |  to virtual machine at JASMIN end  
`login.archer2.ac.uk` |  `hpxfer[34].jasmin.ac.uk` |  to high-performance physical machine at JASMIN end
{.table .table-striped}

### GridFTP over SSH

[GridFTP over SSH]({{% ref "gridftp-ssh-auth" %}}): GridFTP performance with convenience of SSH. Requires persistent ssh agent
on local machine where you have your JASMIN key. **2nd choice method**

_source_ |  _dest_ |  _notes_  
--- | --- | ---
`login.archer2.ac.uk` |  `hpxfer[34].jasmin.ac.uk` | 
{.table .table-striped}

### GridFTP using certificate auth

[GridFTP using certificate auth]({{% ref "gridftp-cert-based-auth" %}}): Fully-featured GridFTP. Suitable for person-not-present transfers & long-
running ARCHER2 workflows. **3rd choice method: legacy technology which will be discontinued on JASMIN in 2025**

Additional requirement:

- you need to have registered the subject of your JASMIN-issued short-term credential with ARCHER2 support.

_source_ |  _dest_ |  _notes_  
--- | --- | ---
`login.archer2.ac.uk` |  `gridftp1.jasmin.ac.uk` |  over 10G JANET.<br>Dedicated GridFTP server.<br>**No need for persistent SSH agent at ARCHER2 end**
{.table .table-striped}

Notes:

- We are currently struggling to get the legacy components working on our new operating system, Rocky 9, so the current service
continues on the old (CentOS7) server `gridftp1` for now, but may need to be withdrawn at short notice.
- Even if/when we succeed in redeploying the service on Rocky 9, we plan to discontinue this service now that a better alternative
is available with Globus.

## 1st choide method: Globus

This is now the recommended method, because:

- it always ensures the best performance
- it is a managed transfer service, less prone to overloading and system issues
- it is actively maintained
- it is easy to use

Because Globus can do transfers between two third-party locations, you don't necessarily
need to invoke the transfers from a machine on JASMIN, or ARCHER2 (even though it's those 
two locations which will be involved as source and destination for the transfer). This could
be done from your laptop or desktop, but could also be done from within a workflow that's running
somewhere (e.g. ARCHER2 or JASMIN).
So, first think about where you want to control the process from.

In **that** location, follow the steps below:

1\. Set up the Globus Command Line interface

- follow the steps [described here]({{% ref "globus-command-line-interface/#initial-setup"%}})

2\. Identify the collections that you want to transfer between, for your transfer:

In this case, these are likely to be:

- the [ARCHER2 filesystems collection](https://app.globus.org/file-manager/collections/3e90d018-0d05-461a-bbaf-aab605283d21/overview), with ID `3e90d018-0d05-461a-bbaf-aab605283d21`
- the [JASMIN default collection](https://app.globus.org/file-manager/collections/a2f53b7f-1b4e-4dce-9b7c-349ae760fee0/overview), with ID `a2f53b7f-1b4e-4dce-9b7c-349ae760fee0`

Set an environment variable for each of these, to avoid having to type the ID each time:
{{<command>}}
export a2c=3e90d018-0d05-461a-bbaf-aab605283d21
export jdc=a2f53b7f-1b4e-4dce-9b7c-349ae760fee0
{{</command>}}

3\. Check access to these collections

These collecitons are restricted-access rather than public, so your access to them is via a series of authentication/authorisation/consent steps which the following actions will guide you through:

{{<command>}}
globus ls $a2c:/~/
(out) (ARCHER2 home directory file listing should appear)
{{</command>}}

{{<command>}}
globus ls $jdc:/~/
(out) (JASMIN home directory file listing should appear)
{{</command>}}

The steps above establish your ability to interact with each of the specified collections using Globus. Once you've completed each one,
you should see a directory listing.

Once you've completed the steps for both source and destination collections, you are ready to try a transfer.

4\. Initiate a simple transfer

{{<command>}}
globus transfer $a2c:/~/1M.dat $jdc:/~/1M.dat
(out)Message: The transfer has been accepted and a task has been created and queued for execution
(out)Task ID: aa0597a4-80a7-11ef-b36b-a1206a7ee65f
{{</command>}}

This should complete quite quickly for a small file, but for a larger file you can check the progress using the task ID.

{{<command>}}
globus task show aa0597a4-80a7-11ef-b36b-a1206a7ee65f
(out)Label:                        None
(out)Task ID:                      aa0597a4-80a7-11ef-b36b-a1206a7ee65f
(out)Is Paused:                    False
(out)Type:                         TRANSFER
(out)Directories:                  0
(out)Files:                        1
(out)Status:                       SUCCEEDED
(out)Request Time:                 2024-10-02T10:18:32+00:00
(out)Faults:                       0
(out)Total Subtasks:               2
(out)Subtasks Succeeded:           2
(out)Subtasks Pending:             0
(out)Subtasks Retrying:            0
(out)Subtasks Failed:              0
(out)Subtasks Canceled:            0
(out)Subtasks Expired:             0
(out)Subtasks with Skipped Errors: 0
(out)Completion Time:              2024-10-02T10:18:39+00:00
(out)Source Endpoint:              Archer2 file systems
(out)Source Endpoint ID:           3e90d018-0d05-461a-bbaf-aab605283d21
(out)Destination Endpoint:         JASMIN Default Collection
(out)Destination Endpoint ID:      a2f53b7f-1b4e-4dce-9b7c-349ae760fee0
(out)Bytes Transferred:            1000000
(out)Bytes Per Second:             148452
{{</command>}}

If you wanted to use the above in a script, and block/wait for the transfer task to complete before 
continuing, you can use `globus task wait <taskid>`, for example:

{{<command>}}
globus task wait aa0597a4-80a7-11ef-b36b-a1206a7ee65f
{{</command>}}

will now return control immediately, since the task has completed.

Globus transfer tasks are aysychronous, submitted to **your own** mini-queue,
where you can have as many queued tasks as you like but only 3 in progress at any one time. This ensures good performance for
all users, but your tasks do not linger in long multi-user queues. The best way to reassure yourself of this is to try it out.

For help with any globus command you can do `globus <command> --help`.

Further examples including sync and automation are given in [Globus command line interface]({{% ref "globus-command-line-interface#examples" %}}), with further examples in the Globus documentation at [https://](https://docs.globus.org/cli/).

Relevant examples:

- [sync with wait](https://github.com/mjpritchard/my-globus-examples/blob/main/sync_wait_simple.sh) using the CLI.
- [Repeatable transfer](https://github.com/mjpritchard/my-globus-examples/blob/main/repeatableTransferWithRefreshTokenStorage.py) using the PythonSDK (more advanced)

Note that Globus transfers (and other actions) can be managed & monitoried by:

- a web interface
- the command-line interface, and
- a Python library

all of which interact with the same underlying service.

NCAS-CMS users should note that work is currently underway to adopt Globus as a drop-in replacement for certificate-based gridftp
in Rose suites currently in use for automating processing and transferring to JASMIN.

## 2nd choice method: gridftp over SSH

The next-best method for transfers between ARCHER2 and JASMIN is using globus-
url-copy with SSH authentication, as described below:

1\. Load your SSH keys for both JASMIN and ARCHER2 on your local machine, then
log in to ARCHER2.

You will need to have loaded into your SSH agent:

- The SSH key associated with your JASMIN account
- The SSH key associated with your ARCHER2 account, if you have one (it is recommended to use a different one than for JASMIN, if so)

You also need to ensure that you connect with the -A option for agent
forwarding, to enable the JASMIN key to be available for the onward
authentication with the JASMIN server.

Note that you do not (and should not) copy your JASMIN private key to ARCHER2.
It should stay on your local machine. This does mean that you need an ssh-
agent running on your local machine, so this method may not work for long-
running continuous processes that need to spawn transfers.

{{<command user="user" host="login.archer2">}}
ssh-add <jasmin ssh key> #(path to your JASMIN ssh key file on your local machine)
ssh-add <archer2 ssh key> #(path to your ARCHER2 ssh key if you have one, on on your local machine)
ssh-add -l # check both keys are loaded (are both key signatures listed in the output?)
ssh -A <archer2-username>@login.archer2.ac.uk
##(ARCHER2 now uses multi-factor auth at this stage)
{{</command>}}

2\. Load the `gct` module (to make the current `globus-url-copy` command
available in the path)

{{<command user="user" host="login.archer2">}}
module load gct
which globus-url-copy
(out)/work/y07/shared/gct/v6.2.20201212/bin/globus-url-copy
{{</command>}}

3\. Transfer a single file to your home directory on JASMIN (limited space,
but to check things work)


{{<command user="user" host="login.archer2">}}
globus-url-copy -vb <file> sshftp://<jasmin-username>@hpxfer1.jasmin.ac.uk/~/<file>
{{</command>}}

Obviously, replace `<file>` with the path to the file you want to transfer.

From here on, the commands are the same as described above in the "1st choice
method" but simply replace

```bash
-cred cred.jasmin gsiftp://gridftp1.jasmin.ac.uk
```

with

```bash
sshftp://<jasmin-username>@hpxfer1.jasmin.ac.uk
```



## 3rd choice method: certificate-based gridftp

{{<alert>}}The use of certificate-based gridtp for transfers to JASMIN has now been replaced by Globus.
Server `gridftp1` will be closed on Friday 13th December 2024 at 16:00
{{</alert>}}

This method for transfers between ARCHER2 and JASMIN uses
globus-url-copy with the concurrency option, as described below, but using
certificate-based authentication rather than SSH. This will work for person-
not-present transfers, so is suitable for long-running processes on ARCHER2
which need to spawn a transfer to JASMIN at intervals up to a month from
initiation.

1\. Load your SSH key for ARCHER2 on your local machine, then log in to
ARCHER2.

This method **does not** require you to use your JASMIN SSH key. It involves:

- obtaining tools to communicate with JASMIN's short-lived credentials service
- using the service to obtain a credential (it should last for 30 days, but a new one can be obtained at any time)
- using the credential to initiate a transfer (this what you would need to repeat for each transfer)

A fuller explanation of the process is given in this document:

- [Data Transfer Tools: GridFTP (certificate-based authentication)]({{% ref "gridftp-cert-based-auth" %}})

Once you have done these steps, you should be able to obtain a short-term
credential as follows (do this command at the ARCHER2 end, after having
downloaded the onlineca script as described in the document mentioned above):

{{<command user="user" host="login.archer2">}}
./onlineca-get-cert-wget.sh -U https://slcs.jasmin.ac.uk/certificate/ -l USERNAME -o ./cred.jasmin
chmod 600 cred.jasmin
{{</command>}}

Note that the path `./` is used for the script `onlineca-get-cert-wget.sh`,
but you should use the path to wherever you saved it. Alternatively, if you
make yourself a `bin` directory and add that to your `PATH`, then you don't
need to specify the path.

2\. Load the `gct` module (to make the current `globus-url-copy` command
available in your path on ARCHER2).

Once loaded, check with `which` to see that you have the `globus-url-copy` command available to you.

{{<command user="user" host="login.archer2">}}
module load gct
which globus-url-copy
(out)/work/y07/shared/gct/v6.2.20201212/bin/globus-url-copy
{{</command>}}

3\. Transfer a single file to your home directory on JASMIN (limited space,
but to check things work)

{{<command user="user" host="login.archer2">}}
globus-url-copy -vb -cred cred.jasmin SRC/FILE gsiftp://gridftp1.jasmin.ac.uk/DEST/FILE
{{</command>}}

Note that we specify the credentials file `cred.jasmin` and use the protocol
`gsiftp://` with no need to specify the username in the connection string
(we've used the path `/~/` to signify "my home directory" as the destination
path). Note also that the hostname in this case, `gridftp1.jasmin.ac.uk` is a
host that you can ONLY connect to directly using gsiftp: it does not permit
SSH connections.

In all other aspects, the transfer is the same as for the SSH method (see "2nd
choice method" below), so the commands below are very similar: we're just
using the gsiftp method instead of sshftp (both are ways of using the gridftp
transfer protocol)

4\. Recursively transfer a directory of files, using the concurrency option
for multiple parallel transfers

{{<command user="user" host="login.archer2">}}
globus-url-copy -vb -cd -r -cc 4 -cred cred.jasmin SRC/DATA/ gsiftp://gridftp1.jasmin.ac.uk/DEST/DATA/
{{</command>}}

**NOTE:** The `-cc` option initiates the parallel transfer of several files at
a time, which achieves good overall transfer rates for recursive directory
transfers. This is different from using the `-p N -fast` options which use
parallel network streams to parallelism the transfer of each file.

The `-p N -fast` options (for parallel-streamed transfers) are not currently
working to all JASMIN storage locations, so use at your own risk until further
notice. The transfer should work OK out of ARCHER2 (check by writing a single
file to `/dev/null` at the JASMIN end) but currently will not work properly
when writing to the SOF storage (`/gws/nopw/j04` or `/gws/nopw/j07`, or
`/work/xfc/vol[1-3]`, though other paths should work OK). This is a known
issue at the JASMIN end, thought to be related to network configuration, which
is still under investigation. Single-stream transfers (omitting the `-p N
-fast` options) should work fine.

Here, the options used are (see `man globus-url-copy` for full details):

```txt
-vb | -verbose-perf 
        During the transfer, display the number of bytes transferred
        and the transfer rate per second.  Show urls being transferred
-concurrency | -cc
      Number of concurrent ftp connections to use for multiple transfers.
-cd | -create-dest
        Create destination directory if needed
-r | -recurse
        Copy files in subdirectories
```

Experiment with different concurrency options (4 is a good start, more than 16
would start to "hog" resources so please consider

5\. Use the sync option to synchronise 2 directories between source and target
file systems:

{{<command user="user" host="login.archer2">}}
globus-url-copy -vb -cd -r -cc 4 -sync -cred cred.jasmin SRC/DATA/ gsiftp://gridftp1.jasmin.ac.uk/DEST/DATA/
{{</command>}}

where `SRC/DATA/` and `/DEST/DATA/` are source and destination paths,
respectively (include trailing slash).

Options are as before but with:

```txt
-sync
        Only transfer files where the destination does not exist or differs
        from the source.  -sync-level controls how to determine if files
        differ
```

Note that the default sync level is 2, see level descriptions below, which
only compares time stamps. **If you want to include a file integrity check
using checksums, you need to use`-sync-level 3` but there may be a performance
cost.**

```txt
-sync-level 
        Choose criteria for determining if files differ when performing a
        sync transfer.  Level 0 will only transfer if the destination does
        not exist.  Level 1 will transfer if the size of the destination
        does not match the size of the source.  Level 2 will transfer if
        the timestamp of the destination is older than the timestamp of the
        source, or the sizes do not match.  Level 3 will perform a checksum of
        the source and destination and transfer if the checksums do not match,
        or the sizes do not match.  The default sync level is 2.
```

So a full sync including comparison of checksums would be:

{{<command user="user" host="login.archer2">}}
globus-url-copy -vb -cd -r -cc 4 -sync -sync-level 3 -cred cred.jasmin src/data/ gsiftp://gridftp1.jasmin.ac.uk/path/dest/data/
{{</command>}}