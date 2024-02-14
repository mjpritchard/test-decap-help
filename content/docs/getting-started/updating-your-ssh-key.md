---
aliases: /article/4834-updating-your-ssh-key
description: How to update your SSH key
slug: updating-your-ssh-key
title: How to update your SSH key
weight: 180
draft: true
---

## Introduction

This article describes how to update the SSH key that you use to login to
JASMIN machines. See [SSH public key authentication]({{< ref "ssh-auth" >}})
for details of how ssh authentication works.

You may need to update your SSH key if:

- You have forgotten the passphrase for your SSH key or have "lost" your key.
- You have switched computers and are unable to copy your original ssh key to the new machine.
- You believe that your SSH private key may have been compromised (for example, you left it in a place that other people could access).

**Do not simply re-upload your old key. This is not secure. You must generate a new one, with a DIFFERENT passphrase, as detailed below.**

If none of the above apply but you are experiencing problems logging in to
JASMIN then we recommend that you read [Login problems?]({{< ref "login-problems" >}}) then contact the
[Helpdesk](http://www.jasmin.ac.uk/help/contact/),
as updating your ssh key may not fix your problems.

Please note that **only one** SSH key can be stored in your JASMIN account.
However, you can copy your SSH key pair to other computers (local to you) to
allow you to login from them, provided that the computer satisfies our network
requirements for security purposes (see [Check network details]({{< ref
"check-network-details" >}})).

## How to update your key

**1\. Generate a new key pair**

To update your SSH key you first need to generate a new key as described here:
[Generate an SSH key pair]({{< ref "generate-ssh-key-pair" >}}). This should
be done on your local machine (e.g. Windows / Linux / Mac). You MUST protect
your key with a strong passphrase. Use a new, different passphrase whenever
you generate a new key.

**2\. Upload the PUBLIC part of the key to your JASMIN account**

Once you have created your new key, you need to upload the public key to your
JASMIN account. If you have followed the suggested key naming convention your
public key should be in file ~/.ssh/id_rsa_jasmin.pub. You can upload it to
your JASMIN account via your [JASMIN profile
page](https://accounts.jasmin.ac.uk/account/profile/). See [Update a JASMIN
account]({{< ref "update-a-jasmin-account" >}}) for more details of how to do
this.

In order to upload your public key, you will need to know your JASMIN Accounts
Portal password, and to look out for the verification code which will be sent
to the email address associated with your JASMIN account.

**3\. Load your new key into your authentication agent on your local machine.**

[This article]({{< ref "login" >}}) describes how to do this and use the key
to log in from the various types of machine (Windows / Mac / Linux) which are
in use.

Once you have uploaded your new public key you need to wait a few minutes
before it will come into effect (allow up to 15 minutes).
