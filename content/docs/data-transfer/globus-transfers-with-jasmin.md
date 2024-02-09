---
aliases: 
- /article/5106-globus-transfers-with-jasmin
- /article/5008-data-transfer-tools-using-the-globus-web-interface
collection: jasmin-documentation
description: Globus transfers with JASMIN
title: Globus transfers with JASMIN
---

This article describes how to do data transfers using JASMIN's **new** Globus
endpoint (now called a **collection** ), based on the most recent version of
[Globus Connect Server](https://www.globus.org/globus-connect-server).

JASMIN's old Globus endpoint, based on
the previous version of the Globus service, ceased operating on 18
December 2023 as support was discontinued by Globus. We have implemented a
new endpoint, based on Globus Connect Server v5.4, with equivalent (but better!)
functionality.

The new collection can be used as a drop-in replacement for the previous
endpoint, aside from a few differences in terminology, and a change to the
authentication process.

## Main differences

There are some differences to how the new (v5) version of Globus works on JASMIN compared to previously:

- Users now interact with a **collection**
- The collection to use is called ["JASMIN Default Collection"](https://app.globus.org/file-manager/collections/a2f53b7f-1b4e-4dce-9b7c-349ae760fee0/overview) and has ID `a2f53b7f-1b4e-4dce-9b7c-349ae760fee0`
- You now use the JASMIN Accounts Portal to authenticate (using your JASMIN account credentials) via OpenID Connect (OIDC). 
- During the authentication process, you are redirected to the JASMIN Accounts Portal to link your Globus identity with your JASMIN account.
- Consent needs to be granted at a number of points in the process to allow the Globus service to carry out actions on your behalf.
- The default lifetime of the authentication granted to your JASMIN account is now **30 days**. After this, you may need to refresh the consent for your "session".
- This service is now available to **all** users of JASMIN: you no longer need to hold the `hpxfer` access role.

The following examples show you how to authenticate with the new JASMIN
Default Collection and list the contents of your home directory. As before,
however, the following file systems are available via this collection

File system  |  Access  
---|---  
`$HOME` (`/home/users/<username>`)  |  Read-write  
`/gws` (group workspaces)  |  Read-write  
`/work/xfc` (transfer cache)  |  Read-write  
`/badc` (CEDA Archive)  
`/neodc` |  Read-only  |  
{.table .table-striped}
  
## List your home directory using the web app

1\. Navigate to <https://app.globus.org>

2\. Log in with your Globus identity (this could be a globusid.org or other
identity)

{{<image src="img/docs/globus-transfers-with-jasmin/file-qEk9SPARZN.png" caption="log in">}}

3\. In File Manager, use the search tool to search for "JASMIN Default
Collection". Select it.

{{<image src="img/docs/globus-transfers-with-jasmin/file-LtMk6bD3Wz.png" caption="Find JASMIN Default Collection">}}

4\. In the transfer pane, you are told that Authentication/Consent is
required. Click Continue.

{{<image src="img/docs/globus-transfers-with-jasmin/file-pprxjkRNiw.png" caption="Consent">}}

5\. Click the link to use the JASMIN Accounts Portal OIDC server to link your
JASMIN identity

6\. You are taken to a page on the JASMIN Accounts portal, where you are
invited to "Authorise" the external application to authenticate and access
your essential account information.

{{<image src="img/docs/globus-transfers-with-jasmin/file-LEssDTYdfN.png" caption="Authorise application">}}

7\. If successful, you are taken back to the Globus web app, where you are
invited to "Allow" the app to use the listed information and services.

{{<image src="img/docs/globus-transfers-with-jasmin/file-lYBGlLIk9A.png" caption="Allow the app to use the info">}}

8\. The directory listing of your home directory should now appear in the
transfer pane.

9\. Try navigating to another collection known to you (previously known as
endpoint) in the other pane and transferring some data. If you have Globus
Connect Personal running locally, you should be able to transfer files to/from
that.

## List your home directory using the command-line interface (CLI)

1\. Load the virtual environment where you have the Globus CLI installed:

(in this example, a Python virtual environment named `~/.globus-cli-venv`
already exists. If it doesn't create one with the command `python3 -m venv
~/.globus-cli-venv` on your local machine). Activate this virtual environment
as follows:

{{<command>}}
source ~/.globus-cli-venv/bin/activate
{{</command>}}

2\. It's recommended to update to the latest version of the CLI by doing the
following:

{{<command>}}
pip install -U globus-cli
{{</command>}}

3\. Check that you have an active globus session and follow any instructions
given, e.g.

{{<command>}}
globus login
globus session show
{{</command>}}

4\. Use the "globus ls" command to list the collection using its ID, starting
at the path of your home directory (/~/)

{{<command>}}
globus ls a2f53b7f-1b4e-4dce-9b7c-349ae760fee0:/~/
{{</command>}}

TIP: you can set the ID of the collection to be an environment variable like
this, for convenience:

{{<command>}}
export JASMIN_GLOBUS=a2f53b7f-1b4e-4dce-9b7c-349ae760fee0
globus ls $JASMIN_GLOBUS:/~/
{{</command>}}

6\. You will be taken through an equivalent set of steps to those needed for
the web app. First off, you will be asked to copy/paste a URL into your
browser and copy/paste back the resulting authentication code.

7\. Once the authentication/consent process has been completed, you should see
a listing of your home directory.

8\. Use the `globus transfer` command to copy data to/from another
**collection** (previously known as endpoint) to your home directory, within
the JASMIN Default Collection. (see `globus transfer --help` for details)
