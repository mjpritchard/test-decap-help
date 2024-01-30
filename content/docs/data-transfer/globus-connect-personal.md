---
aliases: /article/5041-data-transfer-tools-globus-connect-personal
date: 2022-01-25 11:19:40
description: 'Globus Connect Personal'
slug: globus-connect-personal
title: 'Globus Connect Personal'
---

This article describes:

- how to create your own Globus endpoint using Globus Connect Personal

This would enable you to transfer files to/from another Globus Endpoint using
any of the Globus Online transfer tools ([Web app](https://app.globus.org),
[CLI](https://docs.globus.org/cli/) or [Python SDK](https://globus-sdk-
python.readthedocs.io/en/stable/)).

For example, if you set up Globus Connect Personal (GCP) on your
desktop/laptop, you could transfer data files to/from your home directory or
other storage on JASMIN.

**Notes:**

- You may NOT need to do this if your institution already has a Globus endpoint available to you.
- You should NOT install this on a JASMIN server, as a Globus Endpoint is already provided for you.
- If you plan to install it in your user area on your departmental server, check with your local IT administrator whether that's an OK thing to do. Point them at the relevant Globus documentation but note that you should be able to do the install with regular/user privileges and that the software does not need to be left running: it can be started for the duration of any data transfer tasks, then stopped once they have completed.

## Set up Globus Connect Personal on end-user machine

Installers are available for Linux, Mac and Windows operating systems:  

- Linux (command-line) <https://docs.globus.org/how-to/globus-connect-personal-linux/#globus-connect-personal-cli>
- Mac <https://docs.globus.org/how-to/globus-connect-personal-mac/>
- Windows <https://docs.globus.org/how-to/globus-connect-personal-windows/>

The instructions below show the process for Linux (command-line):

These commands should be executed on YOUR OWN MACHINE (not JASMIN):

{{<command>}}
wget https://downloads.globus.org/globus-connect-personal/linux/stable/globusconnectpersonal-latest.tgz
tar xzf globusconnectpersonal-latest.tgz
{{</command>}}

This will produce a versioned globusconnectpersonal directory
Replace `x.y.z` in the line below with the version number you see

{{<command>}}
cd globusconnectpersonal-x.y.z
./globusconnectpersonal
{{</command>}}

Complete the installation using the setup key. If a graphical environment is
detected, a window will appear, to guide you through the steps. If not, text
prompts will appear.

**(Please see the relevant installation guide for your platform, linked above,
for further details)**

## Start Globus Connect Personal (Linux)

{{<command>}}
./globusconnectpersonal -start
{{</command>}}

If you use the web application at <https://app.globus.org>, you should now be
able to see your endpoint listed under "Endpoints" when you filter by
"Administered by me". You can now try listing the files on the endpoint and
perhaps transferring a file to/from one of the Globus Tutorial endpoints using
the web interface.

The setup process will have prompted you for a name for your endpoint. It is
assigned a unique ID, too.

**If you have the Globus Command-Line Interface installed** ([see here]({{<ref "globus-command-line-interface" >}})), you can find
the ID of your own endpoint with the CLI command:

{{<command>}}
globus endpoint search <name> --filter-owner-id <your globus id>
{{</command>}}

If successful, you should now be able to interact with your endpoint via any
of the Globus tools (web app, CLI and Python SDK).

For example, you could list the files on the endpoint:

{{<command>}}
globus ls <endpoint_id>:<path>
{{</command>}}
