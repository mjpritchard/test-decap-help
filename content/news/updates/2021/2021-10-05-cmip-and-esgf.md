---
title: Disseminating essential climate data CMIP and ESGF
date: 2021-10-05 12:33:39+00:00
tags: ['news']
aliases: ['/blog/cmip-and-esgf']
thumbnail: 
icon: fas circle-info
---




The 6th Coupled Model Intercomparison Project ([CMIP6](https://www.wcrp-climate.org/wgcm-cmip)) is an international coordinated effort to understand how the climate has changed in the past and may change in the future. It is the largest climate model intercomparison project to date and is coming to completion. Data produced by CMIP6 is essential to the 2021 assessment report by the Intergovernmental Panel on Climate Change (IPCC). CEDA supports CMIP6 by providing archival, management and publication of all received data and providing analysis capabilities through JASMIN. 


Currently, the CEDA Archive holds approximately three petabytes of [CMIP6 data](https://catalogue.ceda.ac.uk/uuid/b96ce180077f4810abc4eef0e48901d9) (of a total 20 Petabytes produced across the project). Researchers across the world use these important climate projections to explore topics such as the impact of climate change on hydroelectric power in Kenya, how future temperatures will affect human welfare, and many other important science areas. 


Approximately half of the archived data is from the [UK Met Office Hadley Centre](https://www.metoffice.gov.uk/weather/climate/met-office-hadley-centre/index), for which CEDA are the primary archive – this allows all international collaborators access to the Met Office model simulations data. The other half of the data is replicated from other contributing modelling centres from around the world. This replication of internationally produced data allows easy access and analysis for the UK research community.


{{< image src="/img/news/2021/2021-10-05-cmip-and-esgf/cmip.jpg"  caption="Graphic showing how the different experiments in the CMIP project link together" class="rounded" >}}



Figure 1: this shows the continuity between CMIP6 to CMIP7 to CMIPx. Each evolution of the project runs a core set of experiments (the grey thread) and updates the other experiments as climate science evolves. Figure from: [Eyring et al. Overview of the CMIP6 Experimental Design and Organization, GMD, 2016.](https://doi.org/10.5194/gmd-9-1937-2016)  
  



##### Supporting international research


CMIP6 data are shared and published to a globally distributed software infrastructure called the Earth System Grid Federation ([ESGF](https://esgf.llnl.gov/)). This is an international collaboration between research institutions that allows the dissemination of outputs from important climate modelling efforts, such as CMIP6. CEDA is responsible for the UK’s contributions to ESGF. We are part of a network of 33 nodes disseminating climate data around the world by providing tools and interfaces for data management, discovery and download. 


CEDA staff are involved with ESGF in various ways, including; developing software components within the international collaboration, leading the design of future architecture, and maintaining operations for our data node as part of the network. 


##### Automating processes


The sheer volume of data requires the ingestion into the CEDA Archive and subsequent publication to ESGF to be fully automated and flexible enough to work for all incoming data sources. To achieve this, CEDA have developed a dedicated tool called the CEDA REceive-to-Publish Pipeline (CREPP) tool. The tool has successfully been used to publish global climate simulation data of key interest to the climate science community from 30 of the world’s leading climate research institutions.




##### Future architecture for ESGF


In 2019, CEDA [led a](https://zenodo.org/record/3928223#.YTniAi1Q3UY) [programme of work](https://zenodo.org/record/3928223#.YTniAi1Q3UY) to re-engineer the ESGF software system that was first developed over ten years ago. The work included the adoption of new technologies to facilitate cloud deployment. Working with US partners, a first system has been deployed on Amazon Web Services. A deployment by CEDA on JASMIN has been used in a new pilot system integrating tools and systems from other European partners. Work is also focussing on the development of new community standards for functions such as data discovery in order to facilitate interoperability and broader adoption of the systems developed.





