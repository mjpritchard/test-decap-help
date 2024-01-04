---
aliases: /article/848-login-problems
date: 2023-06-13 15:44:56
description: Login problems?
slug: login-problems
tags:
- ssh
- password
- connection
title: Login problems?
---

Having problems connecting to a host on JASMIN? Details of how to login to
JASMIN can be found [here]({{< ref path="docs/getting-started/login" >}}), but this article may help to
diagnose login problems. It provides information for the following issues:

  * Unable to login to a login server e.g. `login1.jasmin.ac.uk`
  * Can login to login server but can't login to a subsequent server
  * ssh-add command gives error: "Could not open a connection to your authentication agent."
  * Errors when trying to connect with MobaXterm

### Unable to login to login server

If you are unable to login to a login server e.g. `login1.jasmin.ac.uk` then
look carefully at any error messages displayed as this can help diagnose what
is wrong:

**1) "Connection reset by peer"**

This suggests a problem with the configuration of your machine or local
network. Connections to JASMIN login servers are allowed from a specific set
list of network domains (the domain is the part **after** the host name e.g.
myhost. **mylocalnetwork.ac.uk** ). For this to happen, 2 things need to be in
place:

  * the IP address of your machine needs to resolve to a full-qualified host name (so that it can be checked against the list)
  * the domain part of the hostname needs to be on JASMIN's allow list.

Use the tool provided on the JASMIN accounts portal to check that your IP
address does indeed resolve:

Visit <https://accounts.jasmin.ac.uk/services/reverse_dns_check/> with your
browser, or do the following at the command line, on the machine from which
you're trying to connect:

    
    
    curl https://accounts.jasmin.ac.uk/services/reverse_dns_check
    

Depending on your system, this will either provide output to the terminal (via
stdout) or on some systems this might save the output in the file
"reverse_dns_check". You may need to look in that file for the result.

See [check network details]({{< ref "check-network-details" >}}) for further
information on how to interpret the result from this.

Most institutional networks for UK universities and partner organisations are
on our allow list, which is updated on request. However if you are trying to
connect from your home broadband, then please be aware that this is not the
the preferred route, for security reasons. If you connect from home, please be
aware that:

  * The IP address which you are allocated by your internet service provider (ISP) may not resolve to a full hostname
  * That domain name is unlikely to be on the allow list.

One solution is to connect via your VPN to your institution first. This
assigns you another IP address belonging to that institution, but you need to
repeat the checks above to make sure that address resolves (not all do).

Another option, if you have SSH terminal access to a machine at your
institution from where you can also make outgoing SSH connections, is that you
connect from your local machine to the machine at your institution, then make
the outward SSH connection to JASMIN from there. In this case, you need to
have your JASMIN SSH key loaded on your local machine first, and remember to
include the -A flag for "agent forwarding" for ALL the intermediate steps.

If all else fails, you can use the ["contingency route"]({{< ref "login-servers" >}}) provide by login2.jasmin.ac.uk (see article for further
details), but you will be limited in what you can do / connect to within
JASMIN as a result. We prefer all users to connect from their institutional
network.

**2) "Permission denied"**

![](file-JdvJWHUysI.png)

Here, the most likely cause is that the SSH key which your client is
presenting does not match the one in your JASMIN account. This can be for a
number of reasons:

  * **You have omitted to specify the username in your SSH connection**
    * In this case, you will be attempting to connect with the username you have on your local machine, which may not be the same.
  * **You have only recently uploaded your SSH key (it can take 20 to 60 minutes before the key propagates to all the places it needs to on JASMIN).**
    * Try waiting a few minutes before trying again.
  * **You don't have your key loaded in your local authentication agent (e.g. ssh-agent).**
    * Check that you are following the method suitable for your operating system 
      * The article "[How to login]({{< ref path="docs/getting-started/login" >}})" has instructions for linux, mac and windows.  

    * Note that connections using NoMachine NX don't require an authentication agent: this can be a good alternative if you're having problems.
  * **You have not yet been granted jasmin-login access or your access has expired.**
    * To check, go to [List my services](https://accounts.jasmin.ac.uk/services/my_services/?page=1&active=1&_apply_filters=1) on the JASMIN accounts portal and check that "Login services: jasmin-login" is listed. If not then you either need to [apply for jasmin-login access](https://accounts.jasmin.ac.uk/account/login/?next=/services/login_services/jasmin-login/), or if you have already done this recently you may simply need to wait for it to be approved. Note that if you have applied for access to a group workspace you still need jasmin-login access in order to connect to jasmin machines.

**3) "The authenticity of host 'nnnn ( <ip address>)' can't be established."
or "key for host nnnn has changed"** ****

Your local computer stores a list of all the other SSH hosts which it has
successfully connected to in the past. If you use an intermediate host like a
login server to make onward connections to a sci machine, the login host will
maintain another such list. In both cases there should be a
file`~/.ssh/known_hosts` (so one in your local home directory on your own
machine, and one in your JASMIIN home directory)

When the SSH client first contacts the host for the SSH connection, it checks
to see if the remote host is one that it recognises. If this check fails, you
may get a message like the following:

**Message 1:**

    
    
    The authenticity of host 'nnnn (<ip address>)' can't be established.
    ECDSA key fingerprint is SHA256:8QY9iBcOQFyEYkpOtBUU8WQGeADb0DyMff01BRuvYls.
    ECDSA key fingerprint is MD5:f9:19:c4:5f:2b:fa:ed:aa:34:86:c9:23:dd:1c:44:30.
    Are you sure you want to continue connecting (yes/no)?
    

**Message 2:**

    
    
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    @       WARNING: POSSIBLE DNS SPOOFING DETECTED!          @
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    The ECDSA host key for nnnn has changed,
    and the key for the corresponding IP address <IP address>
    has a different value. This could either mean that
    DNS SPOOFING is happening or the IP address for the host
    and its host key have changed at the same time.
    Offending key for IP in /home/users/username/.ssh/known_hosts:62
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
    Someone could be eavesdropping on you right now (man-in-the-middle attack)!
    It is also possible that a host key has just been changed.
    The fingerprint for the ECDSA key sent by the remote host is
    SHA256:Evr7U40sEGSLVypfafLYtbF2oYvGDuBxTyrALdx11pk.
    Please contact your system administrator.
    Add correct host key in /home/users/username/.ssh/known_hosts to get rid of this message.
    Offending ECDSA key in /home/users/username/.ssh/known_hosts:115
    ECDSA host key for nnnn has changed and you have requested strict checking.
    Host key verification failed.
    

This can happen when:

  * machines are re-installed
  * when you modify your `~/.ssh/known_hosts` file  

  * when you access a "known" host but via a different name (e.g. `sci1` vs `sci1.jasmin.ac.uk`) 

Message 1 means that you don't have an entry for that host in your
`~/.ssh/known_hosts` file. In most cases, you can safely reply "yes" and the
SSH connection should proceed as normal from then on.

If you get message 2, and are confident that the change is for a legitimate
reason, the solution is to modify your `~/.ssh/known_hosts` file, removing the
entries for that host (there may be more than one, as above for `sci1` vs
`sci1.jasmin.ac.uk`) by deleting those lines. Next time you try and connect,
you will get message 1, but can reply "yes" and the SSH connection should
proceed as normal.

**Note:** If you're using a graphical SFTP or SCP client for data transfers,
the error messages above may be hidden and so it can be harder to establish
the reason for failure. Using a terminal session (in MobaXterm on Windows, or
Mac/Linux terminal) to the problem host will likely reveal the messages and
enable you to follow the steps above to solve the problem.

### Can login to login server but can't login to a subsequent host

Here, there are 3 main possibilities:

**1) You have not set up agent forwarding correctly on your local machine.**

****This allows your ssh key to be used for logging in from jasmin-login1 to
other machines. To check, run the following command on the login server:

    
    
    $ echo "$SSH_AUTH_SOCK"
    

This should display something that looks similar to (but not identical to)
"/tmp/ssh-RNjiHr2844/agent.2844". If nothing is displayed then it indicates
that agent forwarding is not working. Please read 
[how to login]({{< ref path="docs/getting-started/login" >}}) and make sure
 you are running ssh-agent (or similar), have loaded
your private key and are using the -A option on your ssh command for the
connection to the login server. NX users should make sure that the "agent
forwarding" option is ticked when setting up a connection profile.

**2) Some hosts within JASMIN are restricted to particular (groups of)
users.**

The "sci" servers (e.g. `sci1.jasmin.ac.uk`) and "xfer" machines (e.g.
`xfer1.jasmin.ac.uk`) should be available to all with `jasmin-login` access
(see above). However, some other machines are restricted to particular project
participants and require special permission to use. For example, the high-
performance transfer servers `hpxfer[12].jasmin.ac.uk` requires the the
`hpxfer` access role, which can be applied for at the JASMIN accounts portal,
as can most roles currently in use.

**3) There is a problem with the host you are trying to connect to.**

Occasionally there may be problems with the host (machine) which you are
trying to connect to. The sci servers (particularly the high-memory host
jasmin-sci3) experience very high usage loads and occasionally run out of
resources. This may prevent you from logging in. In some circumstances ask you
for a password: this is normally a sign that something is wrong with the
machine, since passwords are not used for host logins on JASMIN, so there is
no point in trying to enter your account password or SSH passphrase at this
point. In this case please contact us using the help beacon below.

If you still have problems then please contact us using the help beacon below.
It would be helpful if you can include as much of the following information as
possible:

  * The IP address and full hostname of the machine you are trying to connect from.
  * The date and time that you tried connecting (to the nearest minute if possible). This will help us to identify any relevant messages in any log files.
  * The exact command you were using
  * Add "-vvv" to your SSH command and send us the the output (please include the SSH command itself)
  * List the SSH keys directory on your local machine. On a linux machine this can be done with the command: "ls -l ~/.ssh"

### ssh-add command gives error: "Could not open a connection to your
authentication agent."

On some terminal sessions the usual instructions for starting the ssh-agent
session and adding the key may give the following error:

    
    
    $ ssh-add ~/.ssh/id_rsa_jasmin
    Could not open a connection to your authentication agent.
    

If you get this error please try either:

modifying the method you use to start the ssh-agent, to:

    
    
    eval $(ssh-agent -s)
    

or see below if using MobaXterm which now has a better way of loading the SSH
key.

### Errors when connecting with Mobaxterm

Please follow the [instructions for MobaXterm]({{< ref "mobaxterm" >}}) (which
include a screen video to show how to load your key into MobAgent).

These instructions have changed with more recent versions of MobaXterm, and
replace the need to use the ssh-add command, so please make sure that both the
version you are using, and your method, are up to date!

Please note that even if your initial connection to (for example) your
university host does not require your JASMIN SSH key, you should still load
the key AND enable agent forwarding, for your initial connection to that host,
so that the key can be used for the subsequent connection to the JASMIN login
host. This actually applies to any connection method, not just MobaXterm.


