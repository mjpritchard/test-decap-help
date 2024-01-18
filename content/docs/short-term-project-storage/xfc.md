---
aliases: /article/4535-xfc
date: 2021-04-22 14:59:13
description: Transfer Cache (XFC)
slug: xfc
title: Transfer Cache (XFC)
---

## What is the XFC?

The Transfer Cache (XFC) provides a large area of temporary storage for
users of JASMIN to store large files and / or a large volume of files on a
short-term basis.

Users are granted a quota of space in their user area on the temporary
storage. When users exceed their quota some of their files will be deleted
automatically.

Users interact with the XFC in two ways:

  1. to initialise their user area, and to get information about their quota, a [command-line client]({{< ref "install-xfc-client" >}}) is used.
  2. to move data in and out of their user area, the standard UNIX command-line tools (cp, mkdir, rm, mv, rsync, etc.) are used.

## Quotas

XFC has two different types of quota. The first is the "hard quota" (HQ). This
is the absolute maximum volume of data that can be stored in the user area.
This is expressed in TB (terabytes).

The second type of quota is the "temporal quota" (TQ). This is expressed in
units of TB day (terabyte days), and has a time component as well as a data
volume component. For an individual file, the TQ for that file is the product
of the size of the file and the number of days the file has been in the user
area. As an example, if the user moves a 2TB file into their area, after 24
hours it will have used 2TB days of the TQ. After 48 hours it will have used
4TB days and after 1 week it will have used 14TB days.

Finally, any file in the XFC can have a maximum persistence of 365 days. i.e.
if a file is in XFC for more than one year then it will be deleted by the
automatic deletion.

{{<image src="img/docs/xfc/file-7mwfbT5NdE.png" caption="">}}

The above figure shows an example of the quota system in use. The red line
shows the temporal quota used (TQ) and the blue line shows the hard quota
(HQ).

  * The user initialises their XFC.
  * On day **5** , the user copies a 1 TB file into their XFC
  * For the next 4 weeks (on days **12** , **19** , **26** and **31** ) the user copies in another 1 TB file
  * The TQ steadily grows until on day **79** it has reached it's limit of 300TB days, the first 1TB file is deleted
  * On day **98** another 1TB file is deleted
  * On day **120** , the user copies 10TB into their XFC
  * On days **122** , **130** and **140** the 1TB files that were copied in on days **19** , **26** and **31** are deleted.
  * On day **151** , the 10TB file is deleted.

### Default Quota values:

The default Hard Quota (HQ) is 10 TB

The default Time Quota (TQ) is 300 TB

So you could store 10TB of data for 30 days before risking the deletion of
data.

Additionally, an overall time limit of 365 days is set for ALL data stored by
a given user. You cannot store any data, no matter how small, for longer than
365 days.

## Automatic deletion

If users exceed either their temporal quota or hard quota, then files in their
user area will be deleted automatically. The deletion process will delete as
many files as necessary to bring the amount of HQ and TQ below the quotas
allocated to the user. Files will be deleted on an age basis. Those files that
were copied into the user area first will be deleted first, with newer files
deleted after these.

The user can be notified which files will be deleted if they switch the option
to be notified on and supply an email address in the XFC client. Files will be
deleted 24 hours after the notification.

If a file is modified between the notification and the scheduled deletion (24
hours later) then the file will not be deleted. However, the automatic
deletion is relentless and it will choose some other file to delete instead.
XFC is not designed as permanent storage and the automatic deletion process
has been designed to discourage long term storage of files on it.

## Using XFC

JASMIN provides access to XFC via a command-line client: `xfc`

Once [installed]({{< ref "install-xfc-client" >}}) into your `$HOME`
directory (using one of the `sci` servers), the `xfc` client can be run on
either the `sci` (`sci[1-8].jasmin.ac.uk`) or `xfer` (`xfer[12].jasmin.ac.uk`)
servers, but should NOT be run on the high-performance transfer servers
`hpxfer[12].jasmin.ac.uk`.

The client is used only for interacting with the service, but is not needed
for accessing the storage it provides. The storage provided is mounted in most
places across JASMIN: the path to your XFC volume is returned by the client in
one of the steps shown below.

Users are expected to use the [xfer servers]({{< ref "transfer-servers" >}})
or a high-performance data transfer service to do any data transfers either
within or in/out of JASMIN. This reduces the load on the `sci` servers which
are for general-purpose interactive computing.

The `xfc` client is used to initialise and then query the status (quota,
scheduled deletions etc) of a user's XFC storage volume:

  1. To see all the available options: `xfc -h`
  2. To initialise your user area: `xfc init`

```
xfc init
** SUCCESS ** - user initiliazed with:  
username: username  
email: user.name@stfc.ac.uk  
quota: 300TB  
path: /work/xfc/vol1/user_cache/username
```

The `path` is the path on the JASMIN system to the user area. Data can be
copied here using standard UNIX command-line tools cp, mv, rsync.
Subdirectories can be created using mkdir. Change read/write permissions on
the directories and files using `chmod`, etc. The user area is just a standard
POSIX directory and so any POSIX commands can be used on it.

  3. To get the user area path again: ` xfc path `

```
/work/xfc/vol1/user_cache/username
```    	

  4. To set the user email for notifications: ` xfc email --email=user.name@stfc.ac.uk `
```
** SUCCESS ** - user email updated to: user.name@stfc.ac.uk
```

  5. To query the email set for the user: `xfc email `
```
user.name@stfc.ac.uk
```
  6. To switch deletion notifications on / off: ` xfc notify `
```
** SUCCESS ** - user notifcations updated to: on
```    	

  7. To see remaining quota: ` xfc quota `
```    
------------------------
Quota for user: username 
------------------------
Temporal Quota (TQ)
  Used : 1.7 TB  
  Allocated : 300.0 TB
  Remaining : 298.3 TB
------------------------  
Hard Quota (HQ)
  Used      : 444.9 GB  
  Allocated : 40.0 TB  
  Remaining : 39.6 TB
```

  8. To see which files are scheduled for deletion: ` xfc schedule `
    
        No files scheduled for deletion
    	

  9. To list the files in your user area: ` xfc list`
    
    user_cache/username/historical/.ftpaccess 
    user_cache/username/historical/00README_catalogue_and_licence.txt 
    user_cache/username/historical/day/atmos/day/r1i1p1/COPY_CURRENT_20150326.txt
    	

Pattern matching can be used to search for a file. This is just a simple
substring search, e.g. ` xfc list -m r1i1p1_19500101-19541231.nc `

```
user_cache/username/historical/day/atmos/day/r1i1p1/v20120907/va/va_day_CMCC-CESM_historical_r1i1p1_19500101-19541231.nc
user_cache/username/historical/day/atmos/day/r1i1p1/v20120907/rsds/rsds_day_CMCC-CESM_historical_r1i1p1_19500101-19541231.nc 
user_cache/username/historical/day/atmos/day/r1i1p1/v20120907/prc/prc_day_CMCC-CESM_historical_r1i1p1_19500101-19541231.nc
```    	

File names are given relative to the `user_cache/ ` directory. To list the
full file path use the `-f ` list option: `xfc list -f`

  10. To predict when the files will be deleted, if no other files are added to the user area, and none of the current files are removed: ` xfc predict`
    
    Quota is predicted to be exceeded on 21 Aug 2019 14:58 by 252.1 GB 
    Files predicted to be deleted  
    user_cache/username/historical/.ftpaccess
    user_cache/username/historical/00README_catalogue_and_licence.txt
    user_cache/username/historical/day/atmos/day/r1i1p1/COPY_CURRENT_20150326.txt
    	

## Example of initial use

Below is a list of commands the user might use in their initial session with
XFC.

### initial setup

    
    xfc init 
    xfc path
    xfc email --email=user.name@email.com
    xfc notify
    	

### copy data

    
    mkdir /subdir
    cp /some/data/path /subdir
    	

### query the quota

    
    xfc quota 
    xfc predict 
    xfc schedule
    	


