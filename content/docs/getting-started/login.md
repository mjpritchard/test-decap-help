---
aliases: /article/187-login
date: 2022-10-27 09:37:13
description: How to login
slug: login
title: How to login
---

This article explains how to login to JASMIN. It covers:

  * Preparing your credentials: loading your private key
  * The JASMIN login servers
  * Logging in to JASMIN
  * X-forwarding for graphical applications (within JASMIN only)
  * Where next?

The instructions below cover the process of logging in using a terminal client
only. For a graphical linux desktop, please see alternative instructions using
[NoMachine NX]({{< ref "graphical-linux-desktop-access-using-nx" >}}).

## Preparing your credentials: loading your SSH private key

In order to log in using SSH, you need to present your SSH private key as your
credential (instead of a username and password). Your private key should
reside **only** on your local machine, so this process of loading your key is
something that you do on that local machine. Even if you connect via a
departmental server, there should be no need to upload your private key to
that machine: the process of loading your key and enabling agent forwarding
should ensure that the key is available to subsequent host(s) in the chain of
SSH "hops".

The details of how to do this can vary depending on whether your local machine
runs Windows, MacOS or Linux.

Whichever system you're using, you will need to use an appropriate tool to
load your private key so that it can be presented at the time of logging in.

**Linux and MacOS users:** `ssh-agent` can be used (see instructions below).

**Windows users:** we recommend the [MobAgent utility within MobaXterm]({{<
ref "mobaxterm" >}}). MobXterm is a linux terminal emulator for Windows.

`ssh-agent` is a utility that stores private keys and makes them available to
other software that use the SSH protocol to connect to remote clients.

There are two stages to loading your private key into `ssh-agent`: starting
the agent and then loading your private key. Use the following commands to do
this:

**IMPORTANT: The dollar symbol '$' at the start of the command line in these
example represents the shell prompt as displayed in your terminal - it does
not need to be typed!**

    
    
    $ eval $(ssh-agent -s)
    $ ssh-add ~/.ssh/id_rsa_jasmin
    Enter passphrase for /home/users/jpax/.ssh/id_rsa_jasmin:
    Identity added: /home/users/jpax/.ssh/id_rsa_jasmin (/home/users/jpax/.ssh/id_rsa_jasmin)
    

When you run the `ssh-add` command you will be prompted to enter the
passphrase that you specified when generating your SSH key pair. (If you use
the c shell, replace the command "eval $(ssh-agent -s)" with "exec ssh-agent
$SHELL")

You can test whether your key has been loaded by using the "-l" option to list
the currently loaded keys in your agent:

    
    
    $ ssh-add -l
    2048 SHA256:iqX3NkPCpschVdqPxVde/ujap2cM0mYaAYYedzBGPaI /Users/jpax/.ssh/id_rsa_jasmin (RSA)
    

This confirms that the key in `id_rsa_jasmin` has been loaded and is ready for
use.

**Notes:**

  * The `ssh-agent` session should persist until killed or until system shutdown, even if you close the terminal in which you set it up.
  * It is very important that you protect your private key with a strong passphrase, known only to you. Keys must not be shared between individuals.
  * If you get an error when attempting the above commands please see [login problems]({{< ref "login-problems" >}}).
  * Your public key will have been automatically propagated by the JASMIN accounts system to all the machines to which you have access rights, so should already be present in the correct place. Do not attempt to place the public key manually on any host within JASMIN: it will get automatically overwritten.

Mac users (OS X Leopard onwards) can optionally benefit from linking the SSH
key to Keychain, which securely stores the passphrase as well. This means that
even after a reboot, your SSH key is always available in any Terminal session
automatically. See `man ssh-add` and look for the `--apple-use-keychain` or
`--apple-load-keychain` options, if available (These replace the now-
deprecated `-K` option).

## The JASMIN login servers

See this article for a [description and listing of the login servers]({{< ref
"login-servers" >}})

## Logging in to JASMIN

Assuming that you have loaded your SSH private key using one of the methods
described above, then you can login to a login server as follows:

    
    
    $ ssh -A <user_id>@<login_server>
    

For example, user "jpax" might login to the JASMIN login server with:

    
    
    $ ssh -A jpax@login1.jasmin.ac.uk
    

The **"-A"** **argument is important** because it enables "agent-forwarding".
This means that your the information about your SSH private key is forwarded
to your remote session on the login server so that you can use it for further
SSH connections. (Windows users can [enable X-forwarding in
MobaXterm](https://mobaxterm.mobatek.net/documentation.html#4_1_6) saved
sessions).

**Can't login?**

  * Check our troubleshooting guide: [login problems]({{< ref "login-problems" >}})

## The login message

When you first login you will see a message that provides some useful
information (see Figure 1).

{{<image src="img/docs/login/file-dKz1hO4aLb.png" caption="The login message shown on login1.jasmin.ac.uk. Note that in this case, the -A option enabling onward connections was omitted.">}}

## X-forwarding for graphical applications (within JASMIN only)

Some applications involve displaying graphical output from a remote server,
typically to display plots or interace with a user interface. You can instruct
your SSH connection to enable forwarding of X-server capability by adding the
`-X` argument to the `ssh` command, as follows:

{{<command user="user" host="localhost">}}
ssh -X <user>@<hostname>
{{</command>}}

Note that the `-X` argument can be used in conjunction with the agent-
forwarding`-A` argument. In some cases the `-Y` option may be needed instead of
`-X`.

Please note that this arrangement sends your graphical output back to your
desktop machine over the network, so **should only be used within JASMIN, not
to your local desktop machine**. A solution has been put in place for a
[graphical linux desktop environment within JASMIN using NoMachine NX]({{< ref
"graphical-linux-desktop-access-using-nx" >}}), removing the need to send X11
graphics over the wide-area network. You are strongly advised to use NX for
any situation which involves graphical output on JASMIN. **Using X11 graphics
over the wide-area network outside of JASMIN is not supported: you will not
get good performance** and this makes inefficient use of shared resources
which can impair performance for other users. **Please use NX instead.** Of
course, you may still need to use X11 graphics to send graphical output back
to your JASMIN-side graphical desktop within JASMIN, but this is OK as it is
all within the JASMIN network.

## Where next?

Having been through all the steps and logged in to JASMIN (well done!) you
will be keen to do some real work. You could try the [general purpose
scientific analysis servers]({{< ref "sci-servers" >}}) to get started. Use
the list presented on the login screen to select a sci server which is not
under heavy usage.

For example, from the JASMIN login server, you might choose to login to
`sci1`:

{{<command user="user" host="login1">}}
ssh <user>@sci1.jasmin.ac.uk
{{</command>}}

If you are asked for a password when trying to login to this second machine,
it indicates that your ssh key is not being forwarded. Please check that you
have used the `-A` option in your initial connection to the login server, or
set up agent forwarding permanently in your SSH client configuration on your
local machine.

**There is no point in trying to enter a password (or even the passphrase
associated with your key) as only an ssh key presented in the way described
above is accepted.**

Note that once you are logged into a login server then you can omit the
`<user_id>@` prefix before the server name for the onward connection, since
your username will be the same on both systems. But there is no harm in
including it anyway, to ensure that you connect as the correct user. As shown
above, the `-A` option is not needed for the onward connection, although there
is no harm in including it.

Remember to log out of the login server in addition to the sci server when you
have finished your work, to get back to your own (local) machine:

{{<command user="user" host="sci1">}}
exit
(out)logout
{{</command>}}
{{<command user="user" host="login1">}}
(out)Connection to sci1.jasmin.ac.uk closed.
exit
(out)logout
{{</command>}}
{{<command user="user" host="localhost">}}
(out)Connection to login1.jasmin.ac.uk closed.
## back on your own/local machine now
{{</command>}}