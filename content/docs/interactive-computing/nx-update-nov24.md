---
description: Update on connecting to NoMachine NX service November 2024 
tags:
- nx
- nomachine
- desktop
- X11
title: NX update November 2024
weight: 55
---

## Good news! Connection problems resolved

We now have a solution to the issues some users had with connecting to the NoMachine NX (graphical linux desktop) service, especially from Windows.

- This involves updating your SSH key to a new algorithm, ECDSA (previously RSA).
- We have updated our accounts system to support these new keys, which can now be used throughout JASMIN.
- So [updating your JASMIN SSH key](#updating-your-key) is the first step, but you then have a choice of connection options.

In these notes, `~/` means "your home directory". On Windows this is also represented by `%USERPROFILE%`.

We will update the full documentation and videos in due course, at which point this page will be removed and you will be redirected to that page from here.

## Key presentation options

The configuration you need depends on how you choose to present your key:

- **File-based method**: specify the location of your key file: no admin permission required.
  
- **Agent-based methods**: load your key into an ssh-agent which persists and can be used for subsequent connections across multiple applications.
  - Compatible agents:
    - Windows 10 or 11:
      - Windows Native OpenSSH client (optional feature, needs admin permissions to enable and start the service for the first time).
      - Pageant (part of the {{<link "https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html" >}}PuTTY suite of SSH tools{{</link>}}).
    - Mac & Linux
      - the built-in ssh-agent should work.

Notes:

  1. MobaXterm's own "MobAgent" is NOT compatible for use as an agent, but MobaXterm itself can be configured to use Pageant as an external agent. Your environment may also depend on the agent for other applications.
  2. PuTTY users will either need to create their new key in the PuTTYgen utility, taking care to select the equivalent options to the command below, or convert their new key into a PuTTY-format `*.ppk` file, for use with Pageant.

## NX Configuration

You will need to check that the settings in `~/.nx/config/player.cfg` match your choice of method. If you modify the file, make sure you do it with the NoMachine application **closed**, otherwise the file will get overwritten as the application closes.

- using the **file-based method** on all platforms requires the default settings, which are:
  ```xml
  <option key="SSH client mode" value="library">
  <option key="SSH Client" value="nxssh.exe"> ("nxssh" on Mac/Linux)
  ```
- using the **agent method** with Windows Native OpenSSH client requires these lines:
  ```xml
    <option key="SSH client mode" value="native" />
    <option key="SSH Client" value="C:\Windows\System32\OpenSSH\ssh.exe" />
  ```
- using the **agent method** on Mac & Linux requires these lines:
  ```xml
  <option key="SSH client mode" value="native" />
  <option key="SSH Client" value="/usr/bin/ssh" />
  ```

- If in doubt, uninstall the NoMachine Enterprise Client application and all its associated folders (`~/.nx` and `~/NoMachine`) and re-install before checking the file again.

## Updating your key

For all the above methods, you are now recommended to update your key to ECDSA: most users' keys on JASMIN are of an older type, RSA.

- Create a new key pair using this command. Save the files `id_ecdsa_jasmin` and `id_ecdsa_jasmin.pub` to your `~/.ssh` directory which is in your home directory on your local machine. Storing in this location avoids permissions problems. Remember, do this command on your local machine: your private key should never leave that machine and must be protected with a strong passphrase. **Do not copy your private key to anywhere on JASMIN**
{{<command>}}
ssh-keygen -m PEM -t ecdsa -b 521 -f ~/.ssh/id_ecdsa_jasmin
{{</command>}}
- The equivalent using PuTTYgen or MobaKeyGen is with these settings: choose these **before** clicking "Generate"
{{< image src="img/docs/generate-ssh-key-pair/puttygen-ecdsa-key.png" caption="Settings for ECDSA key in PuTTYgen (same for MobaKeyGen). Choose settings before clicking Generate." wrapper="col-8 mx-auto">}}
- If you're using an agent, remember to load your new key into that agent, using your usual method (usually `ssh-add <key file>` but depends on the agent).
- **IMPORTANT** Next, [follow these steps]({{% ref "update-a-jasmin-account/#update-ssh-public-key" %}}) to **upload your new public key** to your JASMIN profile in the accounts portal. This will get propagated around JASMIN which can take around 15 mins, so please wait before trying to connect.

## Connecting

- You should now create a new connection profile which uses your new key, or the agent into which you loaded your new key, to connect to one of the JASMIN nx servers.
- Test the onward connection to one of the sci servers, e.g. `sci-vm-01` to ensure it's all working correctly.