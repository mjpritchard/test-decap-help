---
title: Met Office Stratospheric Analyses - New Dynamics
date: 2003-10-28 06:00:00+00:00
tags: ['news']
aliases: ['/blog/met-office-stratospheric-analyses-new-dynamics']
thumbnail: 
icon: fas circle-info
---


```


Met Office Stratospheric Analyses - New Dynamics
------------------------------------------------

The assimilation system that produces the Met Office stratospheric data
will soon be changed to use the New Dynamics (ND) version of the
Unified Model.

The changeover is scheduled for 28th October 2003.

**Users of the data need to be aware of the following points:**

- The data will be ordered from South to North, instead of North to
South.

- As before, the wind components (u and v) will be produced on a grid
that is staggered relative to the mass grid (used for T and z).  The
output fields use the "Arakawa B grid" staggering, as before, even
though the ND model uses a "C grid" staggering. 

- The vertical velocity will be w (dz/dt), rather than omega (dP/dt),
and will be output on the mass grid. 

- Three additional UARS levels will be output (25 instead of 22), up to
0.1 hPa (instead of 0.316 hPa).

If you use the grid definitions in the PP header record, the changes to
the ordering of the data will be transparent, otherwise you will need
modify your programs to allow for those changes.

Access routines are supplied by the Met Office to help users read the
data files.  The original versions were written to access data from the
UARS CDHF, but recent versions also read PP format data, as supplied to
the BADC.  A revised version of the access routines has been written
(version 5c - file name acsasm_v5c.f).  This is very similar to the
previous version (5b), except that it will recognize the new w fields
(as well as omega), and the default settings for field types and number
of levels have been modified for New Dynamics.  VAX/VMS-specific code
(only a few lines) has been deleted.  

At the BADC, the new data files can be found in the current year
assimilated data directory: /badc/ukmo-assim/data/standard/2003/

The associated documentation, as provided by the Met Office is 
available in the assimilated data doc directory: 
/badc/ukmo-assim/doc/ieee_binary/new_dynamics/

The Assimilated data documentation on the BADC Web pages will be updated
shortly.


BADC Support
28th October 2003

```
