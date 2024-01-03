---
aliases: /article/5008-data-transfer-tools-using-the-globus-web-interface
date: 2022-01-25 12:34:03
description: 'Data Transfer Tools: Globus Web Interface'
slug: data-transfer-tools-globus-web-interface
title: 'Data Transfer Tools: Globus Web Interface'
---

This article describes how to transfer data using the Globus Command web
Interface.

It covers:

  1. How to transfer files between two (dummy/tutorial) Globus endpoints
  2. How to use the JASMIN Globus endpoint

Globus is a 3rd-party, cloud-based data transfer service for the research
community. It enables (among many things) efficient bulk data transfer between
2 endpoints, using a variety of tools.

# Prerequisites

  1. For dummy/tutorial endpoints: A web browser and internet connection
  2. For JASMIN Globus endpoint: An active JASMIN user account, with “jasmin-login” and “hpxfer” privileges

# Steps

In summary, the steps involved are as follows, but are explained in detail
below:

  1. Follow [this user guide on how to log in and transfer files between the tutorial endpoints](https://docs.globus.org/how-to/get-started/)
    1. Globus already keeps this excellent guide up to date so we won't repeat it here.
    2. Note that you can create a **Globus ID** with its own username and password, rather than use one of the listed identity providers: this can sometimes be simpler.
  2. For access to the JASMIN Globus Endpoint: 
    1. Use the globus web interface to search for the JASMIN Globus Endpoint
    2. Go to File Manager
    3. In "Collection" start typing to search for "JASMIN Globus Endpoint (jasmin crededntials)"
    4. Click the name to request connection to that endpoint
    5. You will now request a credential from JASMIN Short-Lived Credential Service: slcs.jasmin.ac.uk: Enter your JASMIN username and password (NOT your private key passphrase, but the username and password you would use for the JASMIN Accounts Portal)
    6. Press Authenticate
    7. You should see a directory listing of your JASMIN home directory. If necessary, specify the path `/~/`
    8. Try copying one of your files (use something non-sensitive or create an empty folder!) to the globus tutorial endpoint in the opposite pane of the file manager.
    9. Clean up the files you created / moved to the tutorial endpoint(s). Right-click on a file or folder to bring up menu options which include "delete".

Note the alerts which pop up on the Globus interface as you submit transfer
tasks and when they complete. You can check on the progress of tasks with the
"Activity" menu. You should also see email alerts arrive to the email address
associated with the identity you used to log in to Globus.

Once you have mastered using the web interface, move on to our guide on [Using
the Globus Command Line Interface]({{< ref "data-transfer-tools-globus-command-line-interface" >}}), which also points to help on how to set up your
own Globus endpoint on your own computer using Globus Connect Personal.


