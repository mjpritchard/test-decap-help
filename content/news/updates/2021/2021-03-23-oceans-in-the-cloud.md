---
title: Oceans in the Cloud working interactively with huge datasets using Pangeo
date: 2021-03-23 14:44:29+00:00
tags: ['news', 'jasmin', 'jasmin ceda', 'impact-story']
aliases: ['/blog/oceans-in-the-cloud']
thumbnail: 
icon: fas circle-info
---

The properties of our oceans are changing. The Southern Ocean absorbs more heat than any other ocean and as a consequence of climate change, it is warming at an alarming rate. Warming oceans lead to a decline in Antarctic sea ice, increased ocean freshening, sea-level rise, reduced oxygen and CO2 uptake and slow the vertical exchange of waters. This may bring about increased food scarcity, diseases, extreme weather events, loss of coastal protection, and more. It is therefore extremely important to have a detailed understanding of what could happen in the future with a Southern Ocean that is warmer, less salty and is circulating in different ways.

{{< image src="/img/news/2021/2021-03-23-oceans-in-the-cloud/antarctica-482686_1280.jpg"  caption="Image by Angie Agostino from Pixabay" class="rounded" >}}

These interactions are challenging to simulate accurately in coupled climate models, making it hard to predict changes and consequences.  To understand what the models are simulating well and what not so well, researchers need to undertake detailed data analysis and intercomparison. However, the immense size of these datasets means that simply examining the model output is a technical challenge all of its own. With the help of JASMIN, detailed analysis of the Southern Ocean can be undertaken, using the largest ever climate model dataset (the Coupled Model Intercomparison Project 6 - CMIP6, clocking in at over 90 Petabytes!).
  
Dr Andrew Meijers from the British Antarctic Survey (BAS), has been working with JASMIN’s Community Cloud computing platform to analyse Southern Ocean CMIP6 data. “This is a service unique in the UK, that has allowed me to use cutting edge tools to manipulate and explore the extremely large datasets that make up coupled climate model ensembles. This allows for much faster discovery and analysis than was previously possible”, Andrew explains.  
  
The research deployed a range of tools to create a unique environment on JASMIN’s Community Cloud. The following tools were used:

* [Pangeo](https://pangeo.io/about.html)  - an open-source community platform for data analysis for large Earth science datasets. Pangeo can be deployed on the JASMIN Community Cloud to enable use of the tools mentioned below.
* [Jupyter Notebooks](https://jupyter.org/) - a web application that allows you to create and share documents that contain live code, equations, visualizations and narrative text. The [JASMIN Notebook Service](https://help.jasmin.ac.uk/article/4851-jasmin-notebook-service) uses Jupyter notebook technology.
* Various [Python](https://www.python.org/) tools and packages, such as the [Xarray package](https://pypi.org/project/xarray/) - Python is an open-source programming language which has various packages for data analysis. The xarray package can be used to make working with labelled multi-dimensional arrays simpler and more efficient.
* [Dask](https://dask.org/) - a tool used to scale Python packages. It works with the existing Python ecosystem to scale it to multi-core machines and distributed clusters.

Dr Meijers research combines the powerful Xarray package for the manipulation of gridded datasets with a Dask backend, allowing the relatively seamless manipulation of extremely large datasets using parallel computation in an interactive environment. JASMIN’s Cloud enables users to dynamically deploy a complete working Pangeo environment using a point and click web interface.  This circumvents some of the technical problems involved with setting up such a state of the art interface and allows scientists and researchers to focus on the science rather than deployment issues.  
  
JASMIN services are essential for this type of large scale analysis of climate model data. Andrew’s research looks at how water masses vary between models and how they change their heat/carbon properties under different climate forcing scenarios. This research will help determine how Southern Ocean properties may change in the future, as well as identify areas where models are underperforming (see Figure 1).  This research will ultimately help improve climate models, notably those run by the UK Met Office, and inform governmental and intergovernmental bodies such as the Intergovernmental Panel on Climate Change (IPCC).  It is vital to improve understanding of the Southern Ocean’s properties so that we can better prepare for the challenges society may face in future years. The scale and complexity of the datasets means that it would not have been possible without JASMIN.

To find out how this new, and potentially very powerful, technology could help you get more out of using JASMIN [watch Andrew’s talk here](https://www.ceda.ac.uk/events/jasmin-user-seminar-series/).  
  
 {{< image src="/img/news/2021/2021-03-23-oceans-in-the-cloud/ssp585_cmip6_ensemble_wm_heatcontent_copy.png"  caption="Figure 1: CMIP6 model ensemble average heat content change for various key Southern Ocean water masses south of 20S between the present day and 2100 under the strong climate forcing scenario SSP585. The red line gives the ensemble mean, and the blue envelope one standard deviation around this. This shows that the majority of the warming occurs in the circumpolar deep water, and to a lesser extent in the Antarctic Intermediate and Mode Waters. This is slightly unexpected, as the mode and intermediate waters are traditionally thought to be the water masses where heat is injected into the ocean. The cause of their more modest heat uptake is thought to be due to the thinning of these water masses as the surface ocean warms." class="rounded" >}}**Figure 1:** CMIP6 model ensemble average heat content change for various key Southern Ocean water masses south of 20S between the present day and 2100 under the strong climate forcing scenario SSP585. The red line gives the ensemble mean, and the blue envelope one standard deviation around this. This shows that the majority of the warming occurs in the circumpolar deep water, and to a lesser extent in the Antarctic Intermediate and Mode Waters. This is slightly unexpected, as the mode and intermediate waters are traditionally thought to be the water masses where heat is injected into the ocean. The cause of their more modest heat uptake is thought to be due to the thinning of these water masses as the surface ocean warms.

**Contact:**

For more information about using JASMIN, please contact our [helpdesk](mailto:support@jasmin.ac.uk)To find out more about this work, contact:

Dr. Andrew Meijers, Polar Oceans Deputy Science Leader

PI, ORCHESTRA LTSM

British Antarctic Survey

+44 (0) 1223221383

[andmei@bas.ac.uk](mailto:andmei@bas.ac.uk)
