---
aliases: /article/4832-mobaxterm
date: 2023-03-23 18:19:28
description: MobaXterm (windows terminal client)
slug: mobaxterm
title: MobaXterm (windows terminal client)
---

Windows users are strongly recommended to connect to JASMIN using the freely
available MobaXterm This article provides information about:

  * Downloading and installing MobaXterm
  * Basic usage
  * Setting up MobAgent to store your private key
  * Additional features

## Versions of MobaXterm

The instructions given below are for version 23 of MobaXterm. For other
versions please check the MobaXterm documentation.

The method of configuring MobaXterm to store your private key has changed with
different versions. The recommended method, and an alternative, are shown
below.

## Downloading and installing MobaXterm

Download the free Home edition of
[MobaXterm](https://mobaxterm.mobatek.net/download-home-edition.html).

There are 2 editions available:

  * "Portable" edition (can be installed as a regular user)
  * "Installer" edition (may need admin privileges on your machine)

Both editions should be functionally the same once installed, but your choice
may depend on what level of access you have to your Windows machine.

For the "portable" edition, the contents of the downloaded zip file should be
extracted to a folder (eg. on your Windows desktop) where you can double-click
the executable file "MobaXterm_Personal_xx.x" (where xx.x is the version
number). Note that the "CygUtils.plugin" file should remain in this folder as
this is used for storing settings.

Once opened, MobaXterm presents a screen like this:

{{<image src="img/docs/mobaxterm/file-lpgGvBbrOF.png" caption="initial mobaxterm screen">}}

You can use the "Start local terminal" button or click the "+" tab to open
multiple tabs with a different terminal session in each tab. However, it's
worth setting up MobaXterm so that your private key is held globally, so that
it's available to any new terminal session that you open.

## Enabling MobAgent to store your private key

In order to log in to a remote host (e.g. a jasmin host) you need to present
your private key from where it's stored on your local machine. MobaXterm
provides MobAgent which can store your key for the time you are running
MobaXterm, and can then present the key for you, for any session in any tab,
so you don't have to enter your passphrase for each new tab that you open.

The video below demonstrates this process, or you can follow the screenshots
which follow:

You need to enable MobAgent in MobaXterm's _Settings / Configuration / SSH_ :

{{<image src="img/docs/mobaxterm/file-mL5QchQaBk.png" caption="ssh configuration">}}

To do this:

  * Tick "Use internal SSH agent "MobAgent"
  * UN-tick "Use external Pageant"
  * Click the "+" symbol to locate your private key file (e.g. id_rsa_jasmin)
  * Click OK to save the settings. MobaXterm will now need to restart.
  * When you restart MobaXterm you will be prompted for the passphrase associated with your private key.

{{<image src="img/docs/mobaxterm/file-Ktmdc5zxnP.png" caption="passphrase prompt">}}

Once MobaXterm has started, you can check that your SSH key has been loaded by
clicking on 'Start local terminal' and entering the following command:

**IMPORTANT: in the command examples below, the dollar symbol '$' at the start
of the command line in these example represents the shell prompt as displayed
in your terminal - it does not need to be typed!**

    
    
     $ ssh-add -l
    

You should see something similar to the output below.

    
    
    2048 SHA256:1WgYUGSqffxJX6bWqBZvFsutN3Psjn5mcPV37r6D7vQ Imported-Openssh-Key (RSA)
    

Sometimes the last part of this output shows your email address, but it is
just a comment field at the end of the key, which can be ignored. The fact
that it's returned something which looks like a key, shows that your key is
loaded successfully into the agent.

If you don't see your key listed in output similar to the above, please try
again: perhaps you entered the wrong passphrase? But you will need to succeed
in loading your key before you can connect to JASMIN.

## Logging in to JASMIN using key stored in MobAgent (recommended)

As shown in the video above, once you have set up MobAgent you can connect to
JASMIN by creating a new terminal window. Click the **"Start local terminal"**
button.  
Next, try connecting to the login server:

    
    
    $ ssh -A <user_id>@login2.jasmin.ac.uk
    

(obviously, you need to replace `<user_id>` with your own username on JASMIN,
for example user `jpax` would enter

    
    
    $ ssh -A jpax@login2.jasmin.ac.uk

## Logging in to JASMIN without storing your key in MobAgent

MobAgent provides the most convenient way of accessing JASMIN. However, if you
want to login to JASMIN without setting up MobAgent you can do so as follows.

Click on the 'Start local terminal' button then enter the following commands:

    
    
    $ eval $(ssh-agent -s) 
    ssh-add ~/.ssh/id_rsa_jasmin
    

If your key is named something different, or stored at a different location
than shown above, you will need to specify its location in the ssh-add
command. Note that MobaXterm refers to windows drives as e.g. `/drives/c/`
(with forward slashes). So if you've put your key on your desktop, then the
path to that **might** be `/drives/c/Users/fred/Desttop/id_rsa_jasmin` (if "
**fred** " is your local username on Windows).

You will need to do this each time you open a new terminal session. To connect
to JASMIN:

    
    
    $ ssh -A <user_id>@login2.jasmin.ac.uk
    

Where <user_id> is your JASMIN username.

As you can see, the MobAgent method mentioned previously makes this a bit
easier, because it persists between sessions and you navigate to the location
of your private key using graphical tools instead of having to type the path.

## Additional MobaXterm features

MobaXterm is a comprehensive application that enables many useful features
such as:

  * Saved session configurations
  * X-forwarding / X11 / X server ( **Not recommended on JASMIN** : see [NoMachine NX for graphical linux desktop]({{< ref "graphical-linux-desktop-access-using-nx" >}}) instead)
  * SSH agent forwarding
  * SFTP access (with graphical drag-n-drop)
  * Split-tab mode
  * SSH tunnelling
  * Basic Linux commands such as: `cd, ls, pwd, cat`
  * Command-line transfer utilities: `scp, rsync, wget`

Please see the [MobaXterm
documentation](https://mobaxterm.mobatek.net/documentation.html) for details
on these.


