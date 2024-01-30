---
aliases: /article/3808-data-transfer-tools-gridftp-cert-based-auth
date: 2023-01-26 15:43:26
description: 'Data Transfer Tool: GridFTP (certificate-based authentication)'
slug: gridftp-cert-based-auth
title: 'GridFTP (certificate-based authentication)'
---

This article describes how to transfer data using gridftp with certificate-
based authentication.

{{<alert type="info">}}The `globus-url-copy` command used here should not be confused with the Globus online data transfer service. They used to be associated, but no longer. If you are starting out and looking for a reliable, high-performance transfer method, the recommendation now is to learn about [Globus Transfers with JASMIN](../globus-transfers-with-jasmin) (using the Globus online data transfer service) instead of command-line gridftp as described in this document.{{</alert>}}

## Basics of certificate-based authentication

Gridftp servers commonly use a network of "trust" based on electronic
certificates. In order to make use of a gridftp server at one end of your
proposed transfer, you will need to use a certificate which identifies you as
the user, and which is issued by an identity provider which is "trusted" by
the servers at both ends. The trust between the servers is maintained by the
administrators of the service who will ensure that the necessary certificates
are in place.

The presentation of a valid credential which is trusted by the server at the
other end is merely the authentication step (proving who you are).
Authorisation also needs to follow: you, as a user (identified by the
credential you present) need to be authorised to use the resource at the other
end. You should check with the operator of the other gridftp server to see
what additional steps are required before you can actually perform a transfer.

## Getting a short-term credential

In order to access the JASMIN gridftp server, you can now use your JASMIN
portal account to gain a short-term credential which the server will recognise
to authenticate you. This is the same username and password you would use to
log in to <https://accounts.jasmin.ac.uk> to administer your JASMIN account.
**IT IS NOT YOUR SSH PASSPHRASE.**

Here's what to do:

  1. Download tools to interact with JASMIN's Online Certificate Authority (OnlineCA). You can use these to interact with other OnlineCAs too (not just JASMIN's. These replace the "myproxy-logon" tool previously mentioned here)
  2. Use these tools to: 
    1. "Bootstrap trust" i.e. to setup your local certificate store with those needed to interact with the JASMIN server [First time use only]
    2. Obtain a short-term credential using your JASMIN account details [First time, and to renew your short-term credendial as needed]
  3. Use this short-term credential to authenticate with a remote gridftp server which trusts this credential (for example, the JASMIN gridftp server)

### Download OnlineCA tools

On the machine you intend to use as the transfer client, e.g.
`xfer1.jasmin.ac.uk`, in your JASMIN home directory, download 2 shell scripts
which will interact with the Online CA for you. Make them executable:

    
    
    $ wget https://raw.githubusercontent.com/cedadev/online_ca_client/master/contrail/security/onlineca/client/sh/onlineca-get-cert-wget.sh
    $ wget https://raw.githubusercontent.com/cedadev/online_ca_client/master/contrail/security/onlineca/client/sh/onlineca-get-trustroots-wget.sh
    $ chmod u+x onlineca-get-*.sh
    

View help information for the shell scripts:

    
    
    $ ./onlineca-get-trustroots-wget.sh -h
    $ ./onlineca-get-cert-wget.sh -h
    

Bootstrap trust between your own machine and the JASMIN gridftp server: [First
time only]

    
    
    $ ./onlineca-get-trustroots-wget.sh -U https://slcs.jasmin.ac.uk/trustroots/ -b
    Bootstrapping Short-Lived Credential Service root of trust.
    Trust roots have been installed in /home/users/USERNAME/.globus/certificates.
    

Obtain a credential, to be written to an output file `credfile` using your
JAMSIN Accounts Portal username USERNAME:

    
    
    ./onlineca-get-cert-wget.sh -U https://slcs.jasmin.ac.uk/certificate/ -l USERNAME -o ./cred.jasmin
    

Change the permissions on your newly-created cred.jasmin file so that it's
only readable by you (client software may insist on this):

    
    
    chmod 600 ./cred.jasmin
    

When prompted, enter the password associated with your **JASMIN** account
**(NOT your SSH passphrase)**

This credential obtained by this method is valid by default for 720 hours (30
days), as you can see by inspecting the certificate using the following
command:

    
    
    $ openssl x509 -in cred.jasmin -noout -startdate -enddate
    notBefore=Mar 11 17:32:59 2022 GMT
    notAfter=Apr 10 17:32:59 2022 GMT
    

**This means that you can use this particular certificate for the following
720 hours, but after that you will need to repeat this step to obtain a new
one.**

## Example Gridftp usage (general case, or with a JASMIN host as gridftp
client)

Once you have obtained a valid short-term credential on the client transfer
server, and _assuming that the gridftp server at the remote end of the
transfer recognises and is able to authorize you via this credential_ , then
you should be able to transfer data between the remote end (server) and local
end (client) with commands such as shown below:

Please consult the documentation for the `globus-url-copy` command for the
full range of options and arguments.

Please note that the examples below use a fictitious client **gridftp-
client.localsite.ac.uk** server **gridftp-server.remotesite.ac.uk** which
needs to be replaced in your commands with the hostname of the gridftp server
and client you are actually using.

Check help documentation for the globus-url-copy command:

    
    
    $ globus-url-copy -help
    

1\. Remote directory listing issued by client on `gridftp-
client.localsite.ac.uk` to server `gridftp-server.remotesite.ac.uk` where you
have a home directory `/home/users/USERNAME`:

    
    
    $ globus-url-copy -cred cred.jasmin -vb -list gsiftp://gridftp-server.remotesite.ac.uk/home/users/USERNAME/
    

2\. Download a file from remote directory `/home/users/USERNAME` to
destination on the client machine:

    
    
    $ globus-url-copy -cred cred.jasmin -vb gsiftp://gridftp-server.remotesite.ac.uk/home/users/USERNAME/myfile file:///path/to/localdir/myfile
    

The `-p N` and `-fast` options can additionally be used in combination to
enable `N` parallel streams at once, as shown below. You can experiment with N
in the range 4 to 16 to obtain the best performance, but please be aware that
many parallel transfers can draw heavily on shared resources and degrade
performance for other users:

    
    
    $ globus-url-copy -cred cred.jasmin -vb -p 16 -fast gsiftp://gridftp-server.remotesite.ac.uk/home/users/USERNAME/myfile file:///path/to/localdir/myfile
    

3\. Recursively download the contents of a directory on a remote location to a
local destination.

    
    
    $ globus-url-copy -cred cred.jasmin -vb -p 4 -fast -cc 4 -cd -r gsiftp://gridftp-server.remotesite.ac.uk/home/users/USERNAME/mydir/ file:///path/to/localdir/mydir/
    

Where:

  * `-cc N` requests `N` concurrent transfers (in this case, each with `p=4` parallel streams)
  * `-cd` requests creation of the destination directory if this does not already exist
  * `-r` denotes recursive transfer of directories
  * `-sync` and `-sync-level` options can be used to synchronise data between the two locations, where destination files do not exist or differ (by criteria that can be selected) from corresponding source files. See `-help` option for details.
  * the `file:///` URI is used to specify the destination on the local file system.

## Uploading data

The above commands can also be adapted to invoke transfers from a local source
to a remote destination, i.e. uploading data, since the commands all take the
following general form:

    
    
    $ globus-url-copy [OPTIONS] source-uri desination-uri
    

You can use the above examples by replacing the local machine `gridftp-
client.localsite.ac.uk` with one of the jasmin transfer hosts
`xfer[12].jasmin.ac.uk` as a client, To do this, you first need to be logged
in via SSH to one of these hosts and can initiate a transfer by invoking
`globus-url-copy` in one of the ways above.

  * For high-performance transfer (large volumes and/or longer distances, use `hpxfer[12].jasmin.ac.uk` for which you will need to be registered for the ["hpxfer"](https://accounts.jasmin.ac.uk/services/additional_services/hpxfer/) service. `hpxfer[12].jasmin.ac.uk` are also recommended for transfers to/from ARCHER2. `hpxfer2.jasmin.ac.uk` is tuned for very long path transfers (e.g. Western US or Australia/NZ)
  * For remote hosts using JASMIN's dedicated network links (Leeds, Met Office) use `xfer[12].jasmin.ac.uk` as the client (These are virtual machines so have limited performance, but your transfer will be over a dedicated network connection)

## Connecting to the JASMIN GridFTP server

In order to do transfer using a JASMIN host as the gridftp server (rather than
client), you would need to interact with the JASMIN GridFTP server
`gridftp1.jasmin.ac.uk`. You cannot log in to this server directly via SSH:
you only initiate GridFTP transfers to and from it from another client.

In the following example, a client is initiated on a fictitious remote host
`client.remotesite.ac.uk` and tests the connection by transferring from
/dev/zero on the local machine (at `remotesite` ) to /dev/null on the JASMIN
gridftp server. Note that you can use the SLCS server at JASMIN to obtain the
short-term credential required ( **but the first time, you will need to
download and use the OnlineCA tools as described above** ). You can renew your
credential and perform the test transfer as follows:

    
    
    [username2@remoteclient ~] ./onlineca-get-cert-wget.sh -U https://slcs.jasmin.ac.uk/certificate/ -l USERNAME -o ./cred.jasmin
    [username2@remoteclient ~] $ globus-url-copy -cred cred.jasmin -vb -p 8 -fast /dev/zero gsiftp://gridftp1.jasmin.ac.uk/dev/null
    Source: file:///dev/
    Dest:   gsiftp://gridftp1.jasmin.ac.uk/dev/
      zero  ->  null
    
    4153409536 bytes       792.20 MB/sec avg       792.20 MB/sec inst
    

This server is also used as the JASMIN GridFTP Server globus endpoint, see
[GridFTP transfers using Globus Online]({{< ref "globus-command-line-interface" >}}) (however you can only currently use your CEDA
SLCSs credential with Globus Online. The JASMIN team is working on a solution
for this).

Please note that the servers `xfer[12].jasmin.ac.uk` and
`hpxfer[12].ceda.ac.uk` are not gridftp **servers**. They have the `globus-
url-copy` client installed, so can be used as clients to connect to remote
gridftp servers, and also support [gridftp over SSH]({{< ref "gridftp-ssh-auth" >}}) (both incoming and outgoing), but do not act as
servers for certificate-based gridftp as shown in these examples. The JASMIN
gridftp server for read-write access to home directories and group workspaces
is `gridftp1.jasmin.ac.uk`. Access to this requires [registration for high-
performance data transfer (hpxfer)]({{< ref "hpxfer-access-role" >}}). See
also [Transfer Servers]({{< ref "transfer-servers" >}}).

## Third-party transfers

It should be possible, with the correct configuration at each site, to
initiate on host A a transfer of data between two other gridftp servers B and
C (a third party transfer). Both URIs would use `gsiftp:` as the protocol:

```bash
globus-url-copy -vb -p 4 gsiftp://B/source gsiftp://C/destination
```

Further information can be found in the documentation for globus-url-copy.
However [Globus Online](https://www.globus.org/app/transfer) provides a
managed service to orchestrate and monitor transfers between gridftp endpoints
in a more user-friendly way, so is recommended as an alternative to setting up
third-party transfers manually. See [Data Transfer Tools: using the Globus web interface]({{< ref "globus-web-interface" >}})

## Future plans

As [support for the open-source Globus Toolkit (including globus-url-copy) has
now been withdrawn by Globus](https://www.globus.org/blog/support-open-source-
globus-toolkit-ends-january-2018), the future of direct gridftp transfers is
uncertain. We advise users to spend some time understanding and testing
transfer workflows with the Globus Online (or cloud-based) transfer service,
including the Globus Command-Line and web interfaces and Python SDK as these
are likely to replace direct gridftp in due course.
