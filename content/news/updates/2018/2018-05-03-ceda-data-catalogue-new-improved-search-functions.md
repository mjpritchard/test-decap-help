---
title: CEDA Data Catalogue - new, improved search functions!
date: 2018-05-03 11:25:43+00:00
tags: ['news']
aliases: ['/blog/ceda-data-catalogue-new-improved-search-functions']
thumbnail: 
icon: fas circle-info
---
Finding the right data for your research can often be a daunting task... especially when faced with a vast archive of over 5000 datasets with 180 million files to choose from, such as in the CEDA archive! However, CEDA are pleased to announce a major step towards helping resolve this conundrum; bringing the power of industry search tools and direct metadata harvesting at scale to solve these problems.


The [CEDA Catalogue](http://catalogue.ceda.ac.uk) now allows users to search by "variable". This work builds upon a significant project to scan all data files (100s of millions) in the CEDA Archive and to index the resulting metadata into a single store. CEDA's new data search allows you to search by:


* Variable long names
* Variable CF standard names
* Variable IDs (such as MIP ids)
* Record titles, abstracts, keywords and abbreviations


A free-text search now queries metadata held in titles, abstracts and keywords within the major catalogue records. It also queries the various variable names that are found in the data files. When the user visits the catalogue record, she will see a list of variables (and their associated attributes, such as "units") available for the selected dataset.


For example, through the catalogue search you can generate [a query for "ozone"](http://catalogue.ceda.ac.uk/?q=ozone&record_types=Observation&sort_by=relevance). An example hit will take you [here](http://catalogue.ceda.ac.uk/uuid/c0455ab814224a05ac74642d3d44b73e). Inside the "Variables" tab you will find a list of variables inside the data files, see Figure 1 below.


{{< image src="/img/news/2018/2018-05-03-ceda-data-catalogue-new-improved-search-functions/ozone_keyword_screen_grab.png"  caption="Screenshot of variable tab in the CEDA catalogue records" class="rounded" >}}


*Figure 1. Example of variable tab from the ozone search result on the CEDA catalogue, as described above. The variables tab shows 24 parameters with additional information such as standard names, long names, and units.* 


 


Search results can also be filtered by the different record types in the catalogue and re-ordered based on your preference: by search relevance or in alphabetical order. In addition, variable information is available on dataset records linking long and standard names with variable IDs and units to provide a fuller picture of the data holdings.


This is part of a new, improved search tool on the [CEDA Catalogue](http://catalogue.ceda.ac.uk), which we'll be developing further over the coming months to bring even more enhanced search features. This functionality is new and we encourage users to [share their feedback](mailto:support@ceda.ac.uk "Share feedback with the CEDA team") on how it can be improved.


Using [ElasticSearch technology](https://www.elastic.co/) and harvesting the power of the JASMIN system, this project provides a highly scalable indexing solution that supports a rich and flexible query model. CEDA can now easily join up our extensive data catalogue with variable details harvested directly from each file in the entire archive; resulting in enhanced catalogue search functionality and variable listings on catalogue records.


{{< image src="/img/news/2018/2018-05-03-ceda-data-catalogue-new-improved-search-functions/variable_search_in_ceda_catalogue.png"  caption="Summary of variable search" class="rounded" >}}

