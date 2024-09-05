---
aliases: /article/4997-transfers-from-archer2
description: Transfers from ARCHER2
slug: transfers-from-archer2
title: Transfers from ARCHER2
---

This article explains how to transfer data between ARCHER2 and JASMIN. It
covers:

- The choice of available tools / routes
- Example of how to use the currently-recommended method

## Choice of available Tools/Routes

See [Data Transfer Tools]({{% ref "data-transfer-tools" %}}) for general
details.

Users transferring data between ARCHER2 and JASMIN are often transferring
relatively large sets of data, so it is important to choose the most
appropriate route, method and tools to ensure you get the most efficient and
reliable transfer experience. This can vary depending on system and network
conditions.

If you want to try **all** the options available, you will need:

- [hpxfer](https://accounts.jasmin.ac.uk/services/additional_services/hpxfer/) (high-performance data transfer) access role on JASMIN, in addition to the [jasmin-login](https://accounts.jasmin.ac.uk/services/login_services/jasmin-login/) role.
- a login account at ARCHER2
- (only for certificate-based GridFTP) to have registered the subject of your JASMIN-issued short-term credential with ARCHER2 support.

Check the examples in the linked documentation articles and ensure that you
use them between the hosts used in the examples. Not all services connect over
all routes to/from all hosts!

NOTE:

- Enquiries about access to or use of ARCHER2 should be directed to ARCHER2 support ([support@archer2.ac.uk](mailto:support@archer2.ac.uk))
- Enquiries about access to or use of JASMIN should be directed to JASMIN support (use beacon, below-right or [support@jasmin.ac.uk](mailto:mailto:support@jasmin.ac.uk))


## Available transfer methods

### Basic SSH transfer

[**scp/rsync/sftp**]({{% ref "rsync-scp-sftp" %}}): Simple transfers using easy method, pushing data to general purpose xfer nodes. Convenient, but limited performance.

_source_ |  _dest_ |  _notes_  
--- | --- | ---
`login.archer2.ac.uk` |  `xfer1.jasmin.ac.uk` |  over 10G JANET, but to virtual machine at JASMIN end  
`login.archer2.ac.uk` |  `xfer2.jasmin.ac.uk` |  same  
{.table .table-striped}

### GridFTP over SSH

[GridFTP over SSH]({{% ref "gridftp-ssh-auth" %}}): GridFTP performance with convenience of SSH. Requires persistent ssh agent
on local machine where you have your JASMIN key. **2nd choice method**

_source_ |  _dest_ |  _notes_  
--- | --- | ---
`login.archer2.ac.uk` |  `hpxfer1.jasmin.ac.uk` |  over 10G JANET  
`login.archer2.ac.uk` |  `hpxfer2.jasmin.ac.uk` |  over 10G JANET<br>hpxfer2 is configured for longer distances but can be useful if hpxfer1 is busy
{.table .table-striped}

### GridFTP using certificate auth

[GridFTP using certificate auth]({{% ref "gridftp-cert-based-auth" %}}): Fully-featured GridFTP. Suitable for person-not-present transfers & long-
running ARCHER2 workflows. **1st choice method**

_source_ |  _dest_ |  _notes_  
--- | --- | ---
`login.archer2.ac.uk` |  `gridftp1.jasmin.ac.uk` |  over 10G JANET.<br>Dedicated GridFTP server.<br>**No need for persistent SSH agent at ARCHER2 end**
{.table .table-striped}

## 1st choice method: example

The currently-recommended method for transfers between ARCHER2 and JASMIN is using
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

## 2nd choice method: example

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
