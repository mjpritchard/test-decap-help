---
aliases: /article/3838-ceda-archive
description: CEDA Archive
slug: ceda-archive
title: CEDA Archive
---

This article describes accessing the {{<link "ceda_archive">}}CEDA Archive{{</link>}} from JASMIN:

## Overview

The CEDA Archive provides direct access to thousands of atmospheric, climate
change and earth observation datasets. The Archive is directly accessible as a
file system from the shared science machines on JASMIN.

It is a separate service run by the CEDA team - it is not a JASMIN service.
Therefore, many of the links in this document will take you to the [CEDA
Archive help documentation site](https://help.ceda.ac.uk) (as the information
relates to CEDA Archive services). This is separate from the JASMIN help
documentation site (which is specifically about JASMIN services).

## Register for a CEDA Account

First, you need a CEDA Archive account. If you do not have a CEDA account,
please [follow the steps in this CEDA help
document](https://help.ceda.ac.uk/article/39-ceda-account) to register as a
new CEDA user. It also explains how you can reset your password if you have
forgotten it. When you have made a CEDA account, you will then need to use the CEDA portal to [link
it to your JASMIN account](https://help.ceda.ac.uk/article/5105-linking-your-jasmin-account).

The JASMIN Account Portal deals with the management of access to JASMIN
resources (e.g. compute and storage), whereas
[MyCEDA](https://services.ceda.ac.uk/cedasite/myceda/user/) (the CEDA Accounts
Portal) deals with access to CEDA resources (e.g. access to datasets in the
archives). You will need both accounts linked in order to access CEDA Archive
data from JASMIN - you can check whether your accounts are linked from within
the [CEDA Accounts Portal](https://services-beta.ceda.ac.uk/account/jasmin/).

## Accessing the CEDA Archive on JASMIN servers

Once you have linked your CEDA and JASMIN accounts, you will have access to
large parts of the archive straightaway.

The contents of the CEDA Archive are available on the file system under `/badc`
and `/neodc`. Note: do not access data via any symlinks that point to
`/datacentre/archvol*` - these are not permanent links and may change when data
are migrated to new storage. Please use the archive path names under `/badc` and
`/neodc`. Search the [CEDA data
catalogue](https://help.ceda.ac.uk/article/137-ceda-data-catalogue) for further
details about data held in the archive.

Note: `/badc` is for atmospheric & climate model data, `/neodc` is for earth observation data - they
are named after CEDA's previous archive names (British Atmospheric Data
Centre, and the NERC Earth Observation Data Centre).

Most data on the Archive is open access - however, some datasets are
restricted. You can work this out by looking at the UNIX access groups the
data are within (see below). If your required datasets are restricted, access
to these can be obtained by applying for specific access via the data centre
(see [this article ](https://help.ceda.ac.uk/article/98-accessing-data)for more
details). If direct access is not possible the data can be obtained via
[standard FTP and web-based](https://help.ceda.ac.uk/article/99-download-data-from-ceda-archives)
access methods to the CEDA Archive and transferred to a
suitable group workspace on JASMIN. As the data centres use the same JASMIN
infrastructure the transfer rates are high.

The [CEDA Data Catalogue](https://help.ceda.ac.uk/article/137-ceda-data-catalogue) is a useful tool to find and apply for access to datasets.

## Archive access groups

The UNIX access groups used within the CEDA Archive are listed below with
links to example datasets in the CEDA data catalogue for those wishing to use
them:

- `open` Available to any logged in JASMIN user with a linked CEDA user account. See a full list of available datasets [here](https://catalogue.ceda.ac.uk/?q=&results_per_page=20&sort_by=relevance&permission=restricted).
- `cmip5_research` restricted [CMIP3](https://catalogue.ceda.ac.uk/uuid/72afa18db5988d1be0066a26e09422df) and [CMIP5 ](https://catalogue.ceda.ac.uk/?q=wcrp+cmip5&record_types=Observation&sort_by=relevance)datasets
- `esacat1` Satellite data including [MERIS](https://catalogue.ceda.ac.uk/uuid/f26559a9daeae9e6740811d3b3113716), [MIPAS](https://catalogue.ceda.ac.uk/uuid/4a9da084adf4252752e5fe77a5cfd0a9) and [SCIAMACHY](https://catalogue.ceda.ac.uk/uuid/6877f4f100d22f750b44f4c3b7ada498).
- `ecmwf` Access to the [ECMWF Operational Datasets](https://catalogue.ceda.ac.uk/uuid/c46248046f6ce34fc7660a36d9b10a71).
- `eurosat` Satellite data including [IASI](https://catalogue.ceda.ac.uk/?q=iasi&record_types=ObservationCollection&sort_by=relevance), [AVHRR-3](https://catalogue.ceda.ac.uk/?q=avhrr+3&record_types=ObservationCollection&sort_by=relevance) and [GOME-2](https://catalogue.ceda.ac.uk/?q=gome+2&record_types=ObservationCollection&sort_by=relevance).
- `ukmo_wx `  Met Office observational dataset collections including [LIDARNET](https://catalogue.ceda.ac.uk/uuid/38a6e76871fca4c58d0f831e532bff41), [MIDAS](https://catalogue.ceda.ac.uk/uuid/220a65615218d5c9cc9e4785a3234bd0), [MetDB](https://catalogue.ceda.ac.uk/uuid/8ee156b6ed41b153e85dbf02a4134513) and [NIMROD](https://catalogue.ceda.ac.uk/uuid/82adec1f896af6169112d09cc1174499)
- `ukmo_clim` Climatology datasets from the Met Office, including [Central England Temperature](https://catalogue.ceda.ac.uk/uuid/a946415f9345f6da9bf4c475c19477b6) dataset collection, [HadISST](https://catalogue.ceda.ac.uk/?q=hadisst).
- `byacl` These data have specific restrictions on them meaning that they can't be accessed directly from JASMIN, but can be obtained via FTP and web access.

## Data Licensing

All use of data accessed directly from the CEDA Archive must be used in line
with the relevant data licence in place for the relevant dataset for the
purposes stated in the access application. Data licence information can be
found on the relevant CEDA Data Catalogue page, a link to which can be found
in the `00README_catalogue_and_licence.txt` files found in the archive. For
specific data licences granted for restricted datasets, users should log into
their MyCEDA page to view their granted licence and the associated usage
purpose under which access was granted. **Any required alternative use of the
data beyond the original purpose stated in the original licence application
can only be made with a freshly granted new licence application.**

## Accessing data in the archive

In the example below, the logged-in user is listing the contents of the CRU
data sets within the BADC archive. These are "open" so all logged-in users can
access them:

{{<command user="user" host="sci-vm-01">}}
ls -l /badc/cru/data
(out)total 320
(out)-rw-r-----  1 badc open  396 Feb 18  2015 00README
(out)drwxr-x---  8 badc open 4096 Mar 22 10:32 cru_cy
(out)drwxr-x---  4 badc open 4096 Dec  6  2014 crutem
(out)drwxr-x--- 12 badc open 4096 May  9 14:11 cru_ts
(out)drwxr-x---  3 badc open 4096 Feb 18  2015 PDSI
{{</command>}}

The {{<link "ceda_data">}}CEDA Archive Data Browser{{</link>}} is a good place to start as it gives a web-based view of the data with additional metadata but enables copying & pasting the directory path for use within the JASMIN environment:

{{<image src="img/docs/ceda-archive/ceda-archive-cru.png" caption="ceda archive data browser">}}
