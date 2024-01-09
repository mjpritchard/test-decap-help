---
aliases: /article/230-setting-up-your-jasmin-account-for-access-to-mass
categories:
- MASS
collection: jasmin-documentation
date: 2022-03-24 10:52:27
description: Setting up your JASMIN account for access to MASS
slug: setting-up-your-jasmin-account-for-access-to-mass
title: Setting up your JASMIN account for access to MASS
---

The following notes are written assuming you are using a Linux machine in your
home institution, that you have [applied for a new MASS account]({{< ref "how-to-apply-for-mass-access" >}}), and that you have received an email from the
Met Office Storage Team with your new MASS credentials file attached.

## 1\. Start an ssh-agent on your home institution machine, load your private key, and enter your passphrase when requested.

```
[your machine]$ eval $(ssh-agent -s)
[your machine]$ ssh-add ~/.ssh/id_rsa_jasmin        
[your machine]$ <passphrase>
```

**Note:** it's a good idea to keep your private keys for different systems
separated, so you may want to keep your private key for JASMIN in a separate
file, just move the one created during the process described above to a new
sensible location such as ~/.ssh/jasmin_id_rsa.

## 2\. Test login to the JASMIN login node

**Note:** that the `-A` in the first ssh command is mandatory to enable access
to the client VM, the `-X` enables X11 forwarding and is optional.

```
[your machine]$ ssh -A -X <userid>@login1.jasmin.ac.uk
```

## 3\. Test login to the MASS client dedicated virtual machine

From the login machine, you can then login to the MASS client machine.

**Note:** If you are prompted for a password at this stage, then you have
either not requested additional access to the dedicated client machine, or
access hasn't been approved yet, email the Met Office Service Manager
[monsoon@metoffice.gov.uk](mailto:monsoon@metoffice.gov.uk), to verify that
approval has been granted. Allow a couple of days for this process to happen
after submitting your request for access to the VM.

```
[login1.jasmin.ac.uk]$ ssh -X <userid>@mass-cli.jasmin.ac.uk  
[mass-cli.jasmin.ac.uk]$ echo "Hello World"    
[mass-cli.jasmin.ac.uk]$ exit          
[login1.jasmin.ac.uk]$ exit
```

## 4\. Install your MOOSE credentials file, using the "moo install" command.

You can scp the file via a JASMIN transfer server, make sure the credentials
file is called "moose", and you must run the "moo install" command on mass-
cli.jasmin.ac.uk to set it up for you.

{{< alert type="info" >}}
The external moose client has improved security settings, so **you
must use the `moo install` command** to put your moose credentials file in the
correct place in order to get remote access to work. This can only be done on
the client machine mass-cli.jasmin.ac.uk. The credentials file is also changed
by the running of moo install, so this process can be run only once.
{{< /alert >}}

```
[your machine]$ scp moose <userid>@xfer1.jasmin.ac.uk:~/moose         
[your machine]$ ssh -A -X <userid>@login1.jasmin.ac.uk        
[login1.jasmin.ac.uk]$ ssh -X <userid>@mass-cli.jasmin.ac.uk            
[mass-cli.jasmin.ac.uk]$ ls -l ~/moose  
-rwx------ 1 <userid> users 511 Jul  3 13:45 /home/users/<userid>/moose         
[mass-cli.jasmin.ac.uk]$ moo install  
### passwd, command-id=148593088         
Your password is due to expire in -1 day(s).    
A new password can be generated using 'moo passwd -r'.          
[mass-cli.jasmin.ac.uk]$ ls -l ~/.moosedir/moose  
-rw------- 1 <userid> users 511 Jul  3 13:45 /home/users/<userid>/.moosedir/moose
```

Having run these commands on the client machine, the moose file will have
disappeared from your home directory, but a .moosedir directory will have been
created, this will contain a new moose file, an install.log file, and once you
start making MOOSE queries, a moose-external-client.log will be created.

## 5\. Test that you are able to use the locally installed MOOSE client.
```
[mass-cli.jasmin.ac.uk]$ which moo  
/opt/moose/external-client-version-wrapper/bin/moo   
[mass-cli.jasmin.ac.uk]$ moo si  
<system information appears here>  
[mass-cli.jasmin.ac.uk]$ moo help  
<help details appear here>      
[mass-cli.jasmin.ac.uk]$ moo projlist  
<list of projects appears here>
```

You have now successfully accessed MASS from JASMIN!

If you are new to MOOSE, you might like to read the 
[User Guide]({{< ref "moose-the-mass-client-user-guide" >}}) next.


