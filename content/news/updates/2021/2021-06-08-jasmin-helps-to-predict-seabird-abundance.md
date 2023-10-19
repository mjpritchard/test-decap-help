---
title: JASMIN helps to predict seabird breeding abundance in a changing climate
date: 2021-06-08 10:28:59+00:00
tags: ['news', 'impact-story', 'jasmin', 'ceda-archive']
aliases: ['/blog/jasmin-helps-to-predict-seabird-abundance']
thumbnail: 
icon: fas circle-info
---

Many of us have been to the coast and seen seabirds, but have you ever considered how they might be affected by climate change? The UK is surrounded by important populations of seabirds, including Arctic Tern, Kittiwake, and Puffin, that play a key role as top predators and indicators of the health of marine ecosystems. Like many animals, seabirds are exposed to climate change in both marine and terrestrial environments, but the combined effects are rarely considered. Climate change impacts seabird species through a number of mechanisms; for example, by shifting the distributions of prey species, influencing storminess which affects mortality rates, causing overheating at the nest site, or increasing sea level and reducing available breeding habitat. [CEDA services](https://www.ceda.ac.uk/services/) were used by researchers at the British Trust for Ornithology (BTO) to predict future seabird abundance under both marine and terrestrial climate change, as part of the Marine Protected Area Management and Monitoring ([MarPAMM](https://www.mpa-management.eu/)) project.  



{{< image src="/img/news/2021/2021-06-08-jasmin-helps-to-predict-seabird-abundance/puffin.png"  caption="Image showing a puffin on a cliff. Credit: Jonathan Pie on Unsplash" class="rounded" >}}


*Image showing: A puffin standing on a cliff. Credit: [Jonatan Pie](https://unsplash.com/@r3dmax?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/puffin?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*


BTO researchers analysed the relationship between important marine and terrestrial climate variables (such as sea surface temperature, ocean stratification, precipitation and temperature) and breeding abundance for 19 seabird species. It is important to understand the role of climate variables, such as those that measure how stratified the ocean is, because they can affect the prey species that make up the seabirds’ food supply. The project used [UKCP18](https://catalogue.ceda.ac.uk/uuid/c700e47ca45d4c43b213fe879863d589) data from the CEDA Archive and [oceanographic data](http://marine.gov.scot/information/wider-domain-scottish-shelf-model) from Marine Scotland Science, which provided future climate projections for land and marine regions as well as observed (past) climate data for the UK. 


The researchers used [JASMIN’s LOTUS](https://jasmin.ac.uk/about/services/) cluster to parallelise running Bayesian spatial models to reveal the relationship between seabird abundance and various climate variables. Being able to parallelise the work on JASMIN meant that instead of taking ~380 hours (20 model runs \* 19 species \* ~1hr) to run the models consecutively on a personal machine, the work was completed in just a couple of hours. This greatly sped up a key part of the analysis.



Lead analyst on this research, Dr Jacob Davies, commented: 


*“The ability to access data in the CEDA Archive and parallelise tasks on JASMIN enabled us to get through our analytical workflow much more rapidly than would otherwise have been possible, freeing up machines for other important BTO work. The responsiveness of the JASMIN Helpdesk made getting set up on JASMIN straightforward.”*



The combination of using data held in the CEDA Archive and the analysis power of JASMIN, meant that the research could predict how seabirds may be affected by climate change. Predictions showed a decline in the majority of UK breeding seabirds by 2050 (based on the estimated relationships with climate). Uncertainty in the models was high, but for all but five species (Shag, Common Gull, Lesser Black-backed Gull, Black-headed Gull and Common Tern) the median predicted change showed a decline.



These predictions have been used to inform a climate change vulnerability assessment for the species concerned. The results will be published in a scientific paper later in the year. The team will continue to use JASMIN for future parallelisation work as it saved them much valuable time. 


 


{{< image src="/img/news/2021/2021-06-08-jasmin-helps-to-predict-seabird-abundance/herring-gull.png"  caption="Image showing a juvenile Herring Gull in Weymouth Harbour. Credit: David Bowman" class="rounded" >}}  




*Image showing: A juvenile Herring Gull in Weymouth Harbour. Credit: David Bowman.* 


**Footnotes:**


MarPAMM is an environmental project to develop tools for monitoring and managing a number of protected coastal marine environments in Ireland, Northern Ireland and Western Scotland: <https://www.mpa-management.eu/>



For further information about this work, take a look at this [Twitter thread](https://twitter.com/jdavies826/status/1389988288954515457?s=20). 



The Centre for Environmental Data Analysis (CEDA) provides services on behalf of the Natural Environment Research Council ([NERC](https://nerc.ukri.org/)) via the National Centre for Atmospheric Science ([NCAS](https://ncas.ac.uk/en/)) and the National Centre for Earth Observation ([NCEO](https://www.nceo.ac.uk/)). CEDA is based within [RAL Space](http://www.stfc.ac.uk/ralspace/default.aspx), a department of the Science and Technology Facilities Council ([STFC](https://stfc.ukri.org/)).


 


This work used the JASMIN infrastructure. JASMIN is hosted and managed jointly between STFC's [Scientific Computing Department](https://www.scd.stfc.ac.uk/) and [CEDA](https://www.ceda.ac.uk/). 



**Contact:**


For more information about using JASMIN or data held in the CEDA Archive, please [contact our helpdesk](https://www.ceda.ac.uk/contact/).



To find out more about this work, contact [Dr Jacob Davies](mailto:jacob.davies@bto.org). 



