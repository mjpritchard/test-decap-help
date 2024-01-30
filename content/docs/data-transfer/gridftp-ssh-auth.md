---
aliases: /article/3806-data-transfer-tools-gridftp-ssh-auth
date: 2021-06-16 17:41:08
description: 'Data Transfer Tools: GridFTP (SSH authentication)'
slug: gridftp-ssh-auth
title: 'GridFTP (SSH authentication)'
---

This article describes how to transfer data using GridFTP with SSH
authentication.


{{<alert type="info">}}The `globus-url-copy` command used here should not be confused with the Globus online data transfer service. They used to be associated, but no longer. If you are starting out and looking for a reliable, high-performance transfer method, the recommendation now is to learn about [Globus Transfers with JASMIN](../globus-transfers-with-jasmin) (using the Globus online data transfer service) instead of command-line gridftp as described in this document.{{</alert>}}

## Introduction

GridFTP is the recommended tool for transferring large files or groups of
files across high-speed Wide-Area Networks (WANs). It is commonly used with
certificate-based authentication, but can also take place between suitably
configured* server and client using SSH as the authentication mechanism.

The client may need to have certain ports enabled on the host or institutional firewall if present. Consult your local IT support desk for details and direct them to {{< link "https://gridcf.org/gct-docs/6.2/gridftp/admin/index.html#gridftp-config-overview" >}}Configuring GridFTP{{</link>}}.

SSH-based GridFTP does not enable the full feature set provided by
certificate-based GridFTP and in particular does not work with Globus Online,
which provides useful interfaces and APIs for managing large-scale data
transfers, but still provides a major step up in performance by "filling the
pipe" more efficiently than scp/rsync/sftp, particularly over longer distances
and can do verification and sync operations as part of the transfer.

See also:

- [Transfer servers]({{< ref "transfer-servers" >}}) for details on which servers within JASMIN have GridFTP available.
- [Transfers from ARCHER2]({{< ref "transfers-from-archer2" >}}) for details of different routes affecting your choice of server (since this is the one of the most likely places to which JASMIN users will want to transfer data to/from)

## Establishing a connection

Since you will be using SSH as the authentication mechanism, you should ensure
that your initial connection to the JASIMN transfer server is made with the -A
option enabled, to enable agent forwarding:

    
    
    $ ssh -A username1@hpxfer1.jasmin.ac.uk
    

Note that in order to use `hpxfer[12].jasmin.ac.uk` you will need to have
[high-performance data transfer access]({{< ref "hpxfer-access-role" >}}) on
your JASMIN account. An alternative to try out beforehand, is to use `jasmin-
xfer1.ceda.ac.uk`.

Use the `globus-url-copy` command to list the contents of your home directory
on the remote server (This will only work if you already know that that server
supports GridFTP over SSH). In this case, we are making the connection to a
fictitious server `gridftp.remotesite.ac.uk`:

    
    
    $ globus-url-copy -vb -list sshftp://username2@gridftp.remotesite.ac.uk/
    

If `username` and `username2` are the same (on the different systems, the
`username@` part of the sshftp URI can be omitted.

Note that the URI of the server, in this case
`sshftp://username2@gridftp.remotesite.ac.uk` must come immediately after (as
it is an argument to) the `-list` option. This is particularly important if
you are combining this command with other options.

## Example GridFTP usage

Once you have successfully established that you can connect to the server (as
above), then you should be able to transfer data between the remote end
(server) and local end (client) with commands such as shown below:

As above, if you have the same username on both local and remote systems, then
the `username@` part of the sshftp URI can be omitted.

Please consult the documentation for the `globus-url-copy` command for the
full range of options and arguments.

    
    
    $ globus-url-copy -help
    

See also <http://toolkit.globus.org/toolkit/docs/latest-
stable/gridftp/user/#gridftp-user-basic>

2\. Download a file from remote directory `/home/users/USERNAME` to
destination on the local (client) machine, for example a group workspace on
JASMIN:

    
    
    $ globus-url-copy -vb sshftp://username@gridftp.remotesite.ac.uk/home/users/USERNAME/myfile /group_workspaces/jasmin/myworkspace/myfile
    

The `-p N` and `-fast` options can additionally be used in combination to
enable `N` parallel streams at once, as shown below. You can experiment with N
in the range 4 to 32 to obtain the best performance, but please be aware that
many parallel transfers can draw heavily on shared resources and degrade
performance for other users:

    
    
    $ globus-url-copy -vb -p 16 -fast sshftp://username@gridftp.remotesite.ac.uk/home/users/USERNAME/myfile /group_workspaces/jasmin/myworkspace/myfile
    

3\. Test performance with large files by downloading from /dev/zero on the
remote server to /dev/null locally. This excludes any interaction with either
filesystem and gives an upper limit to the performance that can be achieved at
the time. Repeat with values of N in the range 4 to 32 to compare rates. Note
that the performance takes a while to "ramp up", so you will not see the best
rates if transferring small files individually as the process never gets up to
full speed:

    
    
    $ globus-url-copy -vb -p 16 -fast sshftp://username@gridftp.remotesite.ac.uk/dev/zero /dev/null
    

Press CTRL-C to interrupt the transfer. Alternatively you can specify that the
transfer should continue for a fixed duration in seconds using the `-t`
option. In this example, data is transferred from the remote host
gridftp.remotesite.ac.uk to jasmin-xfer2.ceda.ac.uk.

    
    
    [username@hpxfer1 ~]$ globus-url-copy -p 16 -fast -t 10 -vb sshftp://username2@gridftp.remotesite.ac.uk/dev/zero /dev/null
    Source: sshftp://username2@gridftp.remotesite.ac.uk/dev/
    Dest:   file:///dev/
      zero  ->  null
    
       7797473280 bytes       929.52 MB/sec avg      1024.49 MB/sec inst
    Cancelling copy...
    

Note the transfer rate achieved in Megabytes/second (MB/sec), although for
various reasons this is not to be relied upon as an accurate expectation of
speed for real transfers. However, **you are unlikely to achieve even half of
this data rate via`scp`, `rsync` or `sftp` over the same route**. [Bbcp]({{<
ref "bbcp" >}}) may achieve similar rates, however, and
this is considered by some as easier to use.

4\. Recursively download the contents of a directory on a remote location to a
local destination.

    
    
    $ globus-url-copy -vb -p 4 -fast -cc 4 -cd -r sshftp://username2@gridftp.remotesite.ac.uk/home/users/USERNAME/mydir/ /group_workspaces/jasmin/myworkspace/mydir/
    

Where:

  * `-cc N` requests `N` concurrent transfers (in this case, each with `p=4` parallel streams)
  * `-cd` requests creation of the destination directory if this does not already exist
  * `-r` denotes recursive transfer of directories
  * `-sync` and `-sync-level` options can be used to synchronise data between the two locations, where destination files do not exist or differ (by criteria that can be selected) from corresponding source files. See `-help` option for details.

## Upload data (push data from JASMIN to remote server)

The above commands can also be adapted to invoke transfers from a local source
to a remote destination, i.e. uploading data, since the commands all take the
following general form:

    
    
    $ globus-url-copy [OPTIONS] source-uri desination-uri
    

Be sure to check your connection with the remote machine via a simple SSH
login and then a directory listing as shown above.

## JASMIN host as remote server

So far the examples have used a server within JASMIN as the client in the
GridFTP transfer. The transfer can be reversed so that the client is elsewhere
and the JASMIN host is the server specified in the destination URI. The
following command should work connecting to one of the following transfer
servers: (see also [Transfer Servers]({{< ref "transfer-servers" >}}))

  * `xfer[12].jasmin.ac.uk`
  * `xfer3.jasmin.ac.uk` ([additional access role](https://accounts.jasmin.ac.uk/services/additional_services/xfer-sp) required)
  * `hpxfer[12].jasmin.ac.uk` ([high-performance data transfer access]({{< ref "hpxfer-access-role" >}}) required)

Push data to JASMIN from a remote server:

    
    
    $ globus-url-copy -vb -p 8 -fast mydir/myfile sshftp://username@hpxfer1.jasmin.ac.uk/group_workspaces/jasmin/myworkspace/mydir/
    


