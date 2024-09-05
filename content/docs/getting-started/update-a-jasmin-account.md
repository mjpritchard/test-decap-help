---
aliases:
- /article/4552-update-a-jasmin-account
- /article/4834-updating-your-ssh-key
description: Update a JASMIN account
slug: update-a-jasmin-account
title: Update a JASMIN account
weight: 170
---

This article shows you how to update an active JASMIN account on the JASMIN
accounts portal.

## Update info

**Step 1** : On your {{<link "https://accounts.jasmin.ac.uk/account/profile/">}}profile page{{</link>}}, select "Update info".

{{<image src="img/docs/update-a-jasmin-account/file-Q1fSbTtw5P.png" caption="Update detils">}}

**Step 2** : Once the discipline and degree are updated, click "Update profile"

{{<image src="img/docs/update-a-jasmin-account/file-mM0VZn7Adl.png" caption="Update details">}}

**Step 3** : The updated details are displayed.

{{<image src="img/docs/update-a-jasmin-account/file-kaDzBnKcVy.png" caption="Updated profile">}}

## Update SSH public key

To update your SSH public key, first you need to generate a new SSH key pair as described here: [Generate an SSH key pair]({{% ref "generate-ssh-key-pair" %}}). This should be done on
your local machine (e.g. Windows / Linux / Mac). You MUST protect your key
with a strong passphrase. Then follow step 1 to step 5 to update your SSH
public key. You will be asked for a verification token during this process.
The system will reject any key that it recognises has been used before (across all users) so you must generate a fresh key each time: you cannot recycle an old key.

**Step 1** : On the profile page, select "Update key"

{{<image src="img/docs/update-a-jasmin-account/file-OqvYqVcAXA.png" caption="Update key">}}

**Step 3** On the profile page shown above select "Update  key". Within a few seconds, you should receive a
validation token to your registered email address.

{{<image src="img/docs/update-a-jasmin-account/file-OpQxH5gX8f.png" caption=" ">}}

Step 4: Enter the validation token, **delete the old SSH public key** , and
paste the new SSH public key. Click "Update SSH key".

{{<image src="img/docs/update-a-jasmin-account/file-M0OYgojbCq.png" caption="Confirmation">}}

Step 5: Confirmation is displayed. Please allow 15 minutes before attempting to log in again,
 while the new key becomes active on the JASMIN system.

If you get the message "not a valid ssh public key" please check that you have
copied the text from the `.pub` file and that no newline characters are
included: the public key should be a single line of text.
It can be difficult to see this as the text automatically wraps
itself to fit in the text box.

{{<image src="img/docs/update-a-jasmin-account/file-zUPKLVGhgG.png" caption="Key updated">}}

## Change password

**Step 1** : Go to your username in the top-right corner of the navigation bar.
Select "Change password" from the drop-down menu.

{{<image src="img/docs/update-a-jasmin-account/file-0cgN9AXHNN.png" caption="Select change password from menu">}}

**Step 2** : Enter the new password which must conform to the rules stated. You should ideally generate a strongly random string
in an encrypted password manager and store it securely. Make sure it is NOT the same as your SSH key passphrase.
Re-enter the new password to confirm, then click "Change password"

{{<image src="img/docs/update-a-jasmin-account/file-oSTsBB9mv7.png" caption="Submit new password">}}

## Link CEDA account

Linking your CEDA account to your JASMIN account allows you filesystem access
to data on CEDA Archive. If you need to access data on the CEDA Archive and
you do not have an account, you will need to apply for a 
[CEDA account]({{% ref "ceda-archive#register" %}}).

**Step 1** : On the profile page, select "Link now" which is opposite to the
field "Linked CEDA Account". This will take you to the CEDA accounts portal
page where you need to login.

{{<image src="img/docs/update-a-jasmin-account/file-Zy3ZGr4y6V.png" caption="Login to your CEDA account">}}

**Step** **2** : You will be directed to the page below to authorise JASMIN
accounts portal to link your CEDA account and read CEDA profile information.

{{<image src="img/docs/update-a-jasmin-account/file-WAUGpRHodk.png" caption="Allow access">}}

**Step 3** : Your "Linked CEDA Account" field on your JASMIN account profile
page will be updated with "Linked with `<JASMIN username>`" as shown below

{{<image src="img/docs/update-a-jasmin-account/file-PNsdqVO3bn.png" caption="Updated JASMIN account">}}
