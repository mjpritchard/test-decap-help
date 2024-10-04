---
description: Present your SSH key for an SSH connection
slug: present-ssh-key
title: Present your SSH key
weight: 145
---

There are 2 main ways to present your SSH key when connecting via SSH-based methods:

1. specifying the path to the private key, and entering the passphrase each time
1. **(recommended)** loading the key into an `ssh-agent`, which stores the key ready for any subsequent connections you want to make.

**(2)** is more convenient, because you don't have to repeat the process each time you want to make a new connection, but **(1)** is useful to know for
testing and troubleshooting.

## 1\. Specifying the key location each time

This simply involves including the `-i` option in the SSH command to specify the location of your private key:

(You would type this command in a terminal window on your local computer i.e. desktop/laptop). This might be:

- Windows
  - PowerShell terminal window (no additional software needed)
  - MobaXterm (a 3rd party linux terminal emulator for windows, licence required for continued use)
- Mac: "Terminal" or similar applications
- Linux: "Terminal" or similar applications

{{<command user="user" host="localhost">}}
ssh -i path_to/my_private_key user@remotehost
{{</command>}}

## 2\. Loading your key into an agent

We'll demonstrate the following methods:

- Windows (option 1): use the built-in ssh-agent in Windows OpenSSH Client
- Windows (option 2): MobaXterm (a linux terminal emulator for Windows)
- Mac: "Terminal" application
- Linux: "Terminal" or similar application

### Methods to load your key

{{< nav type="tabs" id="tabs-methods" >}}
  {{< nav-item header="Windows (option 1: built-in OpenSSH client)" show="true">}}

  There are two ways to do this:
  - with graphical tools in Windows
  - via the Windows PowerShell (as administrator)

  The video below shows how to do it via graphical tools:

  [Setting up OpenSSH in Windows](https://youtu.be/Tl631gh4DOU)

  The equivalent steps in Powershell are as follows:

  - Check that the OpenSSH client installed with, either by
    
    - locating "optional features" and finding "OpenSSH Client"
    - if it's not installed, tick the box to select it, then click "Next", then "Add" (and wait: NB this can be slow!)

  - or
    - typing this command in a PowerShell window, as administrator

  {{< command prompt="PS C:\Users\User>" shell="powershell" >}}
  Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH.Client*'
  {{< /command >}}
  
  if it **IS** installed, you'll see something like this:

  {{< command prompt="PS C:\Users\User>" shell="powershell" >}}
  (out)Name  : OpenSSH.Client~~~~0.0.1.0
  (out)State : Installed
  {{< /command >}}

  if it's **NOT** installed, you'll see

  {{< command prompt="PS C:\Users\User>" shell="powershell" >}}
  (out)Name  : OpenSSH.Client~~~~0.0.1.0
  (out)State : NotPresent
  {{< /command >}}

  in which case, note the name and version, and use them in this command:

  {{< command prompt="PS C:\Users\User>" shell="powershell" >}}
  Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
  {{< /command >}}

  Eventually (this can be slow!) you should see:

  {{< command prompt="PS C:\Users\User>" shell="powershell" >}}
  (out)Path          :
  (out)Online        : True
  (out)RestartNeeded : False
  {{< /command >}}

  Now you can set up the OpenSSH client:

  - Set the ssh-agent service so that it starts manually, and start it on this occasion:

  {{< command prompt="PS C:\Users\User>" shell="powershell" >}}
  Get-Service ssh-agent
  Set-Service ssh-agent -StartupType Manual
  Start-Service ssh-agent
  {{</command>}}

  (once you're confident that it's working correctly, you could set `-StartupType Automatic`)

  - Load your key into the ssh-agent

  {{< command prompt="PS C:\Users\User>" shell="powershell" >}}
  ssh-add <path to key>
  (out)Enter passphrase for <path to key>: ## right-click to paste your passphrase, then press return
  (out)2048 SHA256:1WgYUGSqffxJX6bWqBZvFsutN3Psjn5mcPV37r6D7vQ
  (out)Imported-Openssh-Key (RSA)
  {{< /command >}}

  {{< /nav-item >}}
  {{< nav-item header="Windows (option 2: MobaXterm)">}}

  {{< youtube id="nEQB0ztE4yY" title="Windows" autoplay="true" >}}
Notes:
- Remember that you need a licence to use MobaXterm beyond the intial free trial period
- The method shown above does not work with applications outside of MobaXterm (like NoMachine NX or VSCode): you would need to use the Windows OpenSSH client instead to use these with an agent.
  
  The video above shows the following steps to enable MobAgent and load your key:
  
  - Go to `Settings > Configuration > SSH`
  - Tick `Use internal SSH agent "MobAgent"`
  - **Un**-tick `Use external Pageant`
  - Click the `+` symbol to locate your private key file (e.g. `id_rsa_jasmin`)
  - Click OK to save the settings. MobaXterm will now need to restart.
  - When you restart MobaXterm, you will be prompted for the passphrase associated with your private key.
   
  {{< /nav-item >}}
  {{< nav-item header="Mac" >}}
  
  ## Mac

  Mac users (OS X Leopard onwards) can optionally benefit from linking the SSH
  key to Keychain, which securely stores the passphrase as well. This means that
  even after a reboot, your SSH key is always available in any terminal session
  automatically. You can do this by running `ssh-add` with `--apple-use-keychain`:

  {{<command user="user" host="localhost">}}
  ssh-add ~/.ssh/id_rsa_jasmin --apple-use-keychain
  {{</command>}}

  And then by adding the corresponding command with `--apple-load-keychain`  to your `.zshrc` file so
  that it loads it for every new terminal session:

  {{<command user="user" host="localhost">}}
  echo "ssh-add --apple-load-keychain" >> ~/.zshrc
  {{</command>}}

  {{< /nav-item >}}
  {{< nav-item header="Linux">}}
  
  ## Linux

  Some linux terminal and desktop environments provide an ssh-agent as a graphical application: consult the 
  documentation for your system.

  In the absence of a graphical application, you can use the following commands in a terminal session:

  - Start the ssh-agent

  {{<command user="user" host="localhost">}}
  eval $(ssh-agent -s)
  (out)Agent pid 94631
  {{</command>}}

  If the agent starts successfully, a process id (pid) is returned as above.

  - Load the key

  {{< command shell="bash" >}}
  ssh-add <path to key>
  (out)Enter passphrase for <path to key>: ## right-click to paste your passphrase, then press return
  (out)2048 SHA256:1WgYUGSqffxJX6bWqBZvFsutN3Psjn5mcPV37r6D7vQ
  (out)Imported-Openssh-Key (RSA)
  {{< /command >}}

  {{< /nav-item >}}
{{< /nav >}}

  ### Check that your key is loaded

  In all cases, you should now check that the key is loaded and ready to use

  {{< command shell="bash" >}}
  ssh-add -l
  (out)2048 SHA256:1WgYUGSqffxJX6bWqBZvFsutN3Psjn5mcPV37r6D7vQ (fred.bloggs@example.com)
  {{< /command >}}

  If you see output similar to the above, your key is now ready to be used in an SSH connection.
  
  Sometimes the last part of this output shows your email address, but it is
  just a comment field, which can be ignored. The fact
  that it's returned something which looks like a key "fingerprint",
  shows that your key is loaded successfully into the agent.
  
  If you don't see your key listed in output similar to the above, please try
  again: perhaps you entered the wrong passphrase? But you will need to succeed
  in loading your key before you can use it to make an SSH connection.

  Once the key is loaded, it can be used in an SSH connection, but whether this persists between different
  sessions may be dependent on your system configuration.


