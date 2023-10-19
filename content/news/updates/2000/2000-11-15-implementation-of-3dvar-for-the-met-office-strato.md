---
title: Implementation of 3DVAR for the Met Office Stratospheric Analyses
date: 2000-11-15 06:00:00+00:00
tags: ['news']
aliases: ['/blog/implementation-of-3dvar-for-the-met-office-strato']
thumbnail: 
icon: fas circle-info
---


```


Implementation of 3DVAR for the Met Office Stratospheric Analyses
=================================================================

The Middle Atmospheric Group at the Met Office has "been working on the 
development of a 3D variational (3DVAR) data assimilation
system to replace the Analysis Correction (AC) data assimilation
system.  The stratospheric analyses were produced by a research data
assimilation from October 1991, and from October 1995 the research
system was replaced by a similar system which was run as part of the
operational suite. "
The new 3DVAR assimilation went operational on 14th November this year.
Output from the new system is now available at the BADC for scientific
research, in the same format as output from the current system.

"The major changes are:

* The introduction of the 3D variational data assimilation scheme.  This
is described by the recent paper by Lorenc et al, 2000 (Quart. J. Roy.
Meteor.  Soc., 126, 2992-3012).

* The assimilation of radiances, rather than temperature retrievals,
from polar orbiter satellites.

* The use of a new model configuration, with 40 (rather than 42) levels;
this is closer to what is used in the standard global forecast model.

Preliminary trials of the new data assimilation system have indicated
that the analysed fields in the troposphere and lower stratosphere are
similar to those from the current system.  Objective forecast verification 
scores have indicated significant benefit from the change from AC (with
assimilation of retrievals) to the use of 3DVAR (with radiance assimilation).  
In the upper stratosphere the changes are more marked: the stratopause is 
typically 10 K warmer than in the current system, with the uppermost levels
cooler.  These latter changes are are largely a reversal of biases that
were introduced inadvertently in January 1999 when the ozone climatology
file was changed incorrectly."


A new filename convention has been adopted to differentiate the output
files from the new 3DVAR assimilation scheme and the data files from the
previous AC data assimilation system. Hence
ppassm_operf_y.._m.._d.._h...pp   becomes
ppassm_operg_y.._m.._d.._h...pp

At the BADC, the new data files can be found in the current year
assimilated data directory: /badc/ukmo-assim/data/standard/2000/
The Assimilated data documentation on the BADC Web pages will be updated
shortly.


BADC Support
15th November 2000

```
